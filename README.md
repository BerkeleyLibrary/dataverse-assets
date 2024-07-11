# Branding changes

See [Dataverse's "Branding Your Installation"](https://guides.dataverse.org/en/latest/installation/config.html#branding-your-installation) documentation.

## Logos

- Create ‘/usr/local/payara6/glassfish/domains/domain1/docroot/logos/navbar/'
- Copy contents of logos/navbar to new directory
- run either:
    - 'curl -X PUT -d '/logos/navbar/dataverse_logo_prod.png' http://localhost:8080/api/admin/settings/:LogoCustomizationFile'
    - 'curl -X PUT -d '/logos/navbar/dataverse_logo_staging.png' http://localhost:8080/api/admin/settings/:LogoCustomizationFile'

## Custom footer
**TODO**: this could go in /home/dataverse instead

- Create '/var/www/dataverse/branding'
- Upload custom-footer.html to new directory
- Run 'curl -X PUT -d '/var/www/dataverse/branding/custom-footer.html' http://localhost:8080/api/admin/settings/:FooterCustomizationFile'

## Custom stylesheet
**TODO**: this could go in /home/dataverse instead

- Upload custom-stylesheet.css to /var/www/dataverse/branding
- Run 'curl -X PUT -d '/var/www/dataverse/branding/custom-stylesheet.css' http://localhost:8080/api/admin/settings/:StyleCustomizationFile'

## Adding “About” to the nav bar
- Run curl -X PUT -d https://docs.google.com/document/d/1aJ5uHj2-J9ARUWFcov5LASsjE0GaLmWMlYkx5OS5kgo/edit?usp=sharing http://localhost:8080/api/admin/settings/:NavbarAboutUrl

## Add text to copyright
- Run curl -X PUT -d ", UC Regents" http://localhost:8080/api/admin/settings/:FooterCopyright