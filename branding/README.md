# Branding changes

## Logos

- Create ‘/usr/local/payara6/glassfish/domains/domain1/docroot/logos/navbar/'
- Upload logo(s) to new directory
- run 'curl -X PUT -d '/logos/navbar/logo.png' http://localhost:8080/api/admin/settings/:LogoCustomizationFile'

## Custom footer
- Create '/var/www/dataverse/branding'
- Upload custom-footer.html to new directory
- Run 'curl -X PUT -d '/var/www/dataverse/branding/custom-footer.html' http://localhost:8080/api/admin/settings/:FooterCustomizationFile'

## Custom stylesheet
- Upload custom-stylesheet.css to /var/www/dataverse/branding
- Run 'curl -X PUT -d '/var/www/dataverse/branding/custom-stylesheet.css' http://localhost:8080/api/admin/settings/:StyleCustomizationFile'

## Adding “About” to the nav bar
- Run curl -X PUT -d https://docs.google.com/document/d/1aJ5uHj2-J9ARUWFcov5LASsjE0GaLmWMlYkx5OS5kgo/edit?usp=sharing http://localhost:8080/api/admin/settings/:NavbarAboutUrl

## Add text to copyright
- Run curl -X PUT -d ", UC Regents" http://localhost:8080/api/admin/settings/:FooterCopyright