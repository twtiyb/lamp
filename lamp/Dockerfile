FROM linuxconfig/apache
MAINTAINER twtiy <twtiyb@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# Main package installation
RUN apt-get update
RUN apt-get -y install supervisor libapache2-mod-php5 php5-mysql mysql-server

# Extra package installation
RUN apt-get -y install php5-gd php-apc php5-mcrypt

# Configure MySQL
RUN sed -i 's/bind-address/#bind-address/' /etc/mysql/my.cnf

# Include supervisor configuration
ADD supervisor-lamp.conf /etc/supervisor/conf.d/
ADD supervisord.conf /etc/supervisor/
 
# Create new MySQL admin user
RUN service mysql start; mysql -u root -e "CREATE USER 'admin'@'%' IDENTIFIED BY 'pass';";mysql -u root -e "GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' WITH GRANT OPTION;"; 

# Allow ports
EXPOSE 80 3306

# VOLUME
VOLUME /var/www/html/

# Start supervisor
CMD ["supervisord"]
