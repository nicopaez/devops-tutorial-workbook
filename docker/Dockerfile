FROM ruby:2.2.0

RUN mkdir -p /var/www
WORKDIR /var/www
RUN git clone https://github.com/nicopaez/pingapp.git /var/www/pingapp

WORKDIR /var/www/pingapp

RUN git checkout master

RUN bundle install --system --without test development

EXPOSE 4567

CMD ["ruby", "app.rb", "-o", "0.0.0.0"]
