# Utiliser l'image PHP 8.1 avec Apache pour Symfony
FROM php:8.2-apache

# Installer les dépendances requises pour Symfony et MySQL
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libpq-dev \
    libonig-dev \
    libzip-dev \
    zip \
    libxml2-dev \
    curl \
    && docker-php-ext-install pdo pdo_mysql zip xml mbstring dom

# Activer mod_rewrite pour Symfony (Apache)
RUN a2enmod rewrite

# Configurer le ServerName pour supprimer l'avertissement
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

# Ajouter la configuration Apache pour Symfony
RUN echo "<VirtualHost *:80>\n\
    ServerAdmin webmaster@localhost\n\
    DocumentRoot /var/www/html/public\n\
    <Directory /var/www/html/public>\n\
        AllowOverride All\n\
        Require all granted\n\
    </Directory>\n\
    ErrorLog \${APACHE_LOG_DIR}/error.log\n\
    CustomLog \${APACHE_LOG_DIR}/access.log combined\n\
</VirtualHost>" > /etc/apache2/sites-available/000-default.conf

# Installer Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Définir le répertoire de travail
WORKDIR /var/www/html

# Installer les dépendances Composer
COPY composer.json composer.lock ./
RUN composer install --no-scripts --no-autoloader

# Donner les bonnes permissions à Apache pour accéder au projet Symfony
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

# Exposer le port 80
EXPOSE 80

# Commande pour démarrer Apache
CMD ["apache2-foreground"]
