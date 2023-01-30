
-include .env

start:
	@hugo server --port 9000 --bind 0.0.0.0

re-build:
	hugo -D

public:
	aws s3 sync /app/www-docs/public s3://docs.site.devpanel.com