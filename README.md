# UC Berkeley Library Dataverse assets 

These are files used to customize the UC Berkeley Library Dataverse's user interface elements. Other than changes made in the Dataverse admin UI (e.g. names of Dataverse collections), these fall into two primary buckets: branding and styling changes, and changes to locale files.

## Branding changes

See [Dataverse's "Branding Your Installation"](https://guides.dataverse.org/en/latest/installation/config.html#branding-your-installation) documentation.

### Logos

- Create ‘/usr/local/payara6/glassfish/domains/domain1/docroot/logos/navbar/'
- Copy contents of logos/navbar to new directory
- run either:
    - 'curl -X PUT -d '/logos/navbar/dataverse_logo_prod.png' http://localhost:8080/api/admin/settings/:LogoCustomizationFile'
    - 'curl -X PUT -d '/logos/navbar/dataverse_logo_staging.png' http://localhost:8080/api/admin/settings/:LogoCustomizationFile'

### Custom footer
**TODO**: this could go in /home/dataverse instead

- Create '/var/www/dataverse/branding'
- Upload branding/custom-footer.html to new directory
- Run 'curl -X PUT -d '/var/www/dataverse/branding/custom-footer.html' http://localhost:8080/api/admin/settings/:FooterCustomizationFile'

### Custom stylesheet
**TODO**: this could go in /home/dataverse instead

- Upload custom-stylesheet.css to /var/www/dataverse/branding
- Run 'curl -X PUT -d '/var/www/dataverse/branding/custom-stylesheet.css' http://localhost:8080/api/admin/settings/:StyleCustomizationFile'

### Google Analytics snippet (production only)
**TODO**: this could go in /home/dataverse instead

- upload analytics-code.html to /var/www/dataverse/branding
- Run 'curl -X PUT -d '/var/www/dataverse/branding/analytics-code.html' http://localhost:8080/api/admin/settings/:WebAnalyticsCode' 

### Add terms of use
**TODO**: this could go in /home/dataverse instead

- upload terms-of-use.html to /var/www/dataverse/branding
- Run 'curl -X PUT -d@'/var/www/dataverse/branding/terms-of-use.html' http://localhost:8080/api/admin/settings/:ApplicationTermsOfUse' 

### Add custom home page
**TODO**: this could go in /home/dataverse instead

- upload custom-homepage.html to /var/www/dataverse/branding
- Run 'curl -X PUT -d@'/var/www/dataverse/branding/custom-homepage.html' http://localhost:8080/api/admin/settings/:HomePageCustomizationFile'

### Adding “About” to the nav bar
- Run curl -X PUT -d https://docs.google.com/document/d/1aJ5uHj2-J9ARUWFcov5LASsjE0GaLmWMlYkx5OS5kgo/edit http://localhost:8080/api/admin/settings/:NavbarAboutUrl

### Changing user guide navbar link to point to Terms of Use
- Run curl -X PUT -d https://docs.google.com/document/d/1H53gxigoKSj3_MmFbgD1hOgU5OAezs_XlDvmh3i4UFM/edit http://localhost:8080/api/admin/settings/:NavbarGuidesUrl
- Update locale files as described below

### Add text to copyright
- Run curl -X PUT -d " The Regents of the University of California" http://localhost:8080/api/admin/settings/:FooterCopyright

## Locale files

Many display strings are managed in the Dataverse's locale files. See upstream [Internationalization](https://guides.dataverse.org/en/latest/installation/config.html#internationalization) documentation.

### Likely deployment path

Presuming that this repo is checked out or accessible from /home/dataverse/dataverse-assets:

- Run ./asadmin create-jvm-options '-Ddataverse.lang.directory=/home/dataverse/dataverse-assets/langBundles'
- Run ./asadmin create-jvm-options '-Duser.variant=x-ucb'
- Restart Dataverse (`systemctl restart payara.service`)