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

### Adding “About” to the nav bar
- Run curl -X PUT -d https://docs.google.com/document/d/1aJ5uHj2-J9ARUWFcov5LASsjE0GaLmWMlYkx5OS5kgo/edit?usp=sharing http://localhost:8080/api/admin/settings/:NavbarAboutUrl

### Add text to copyright
- Run curl -X PUT -d ", UC Regents" http://localhost:8080/api/admin/settings/:FooterCopyright

## Locale files

Many display strings are managed in the Dataverse's locale files. See upstream [Internationalization](https://guides.dataverse.org/en/latest/installation/config.html#internationalization) documentation.

### Likely deployment path

Presuming that this repo is checked out or accessible from /home/dataverse/dataverse-assets:

- Run ./asadmin create-jvm-options '-Ddataverse.lang.directory=/home/dataverse/dataverse-assets/langBundles'
- Restart Dataverse

### Manual process

- Run mkdir /tmp/languages
- Run cp -R langBundles/*.properties /tmp/languages
- Run cd /tmp/languages
- Run zip languages.zip *.properties
- Run curl http://localhost:8080/api/admin/datasetfield/loadpropertyfiles -X POST --upload-file /tmp/languages/languages.zip -H "Content-Type: application/zip"

### Updating locale files from upstream

This should only be necessary when you upgrade Dataverse.

- Run git clone https://github.com/GlobalDataverseCommunityConsortium/dataverse-language-packs.git ; cd dataverse-language-packs
- Run git checkout dataverse-v6.1 (or whatever the appropriate tag is for youer version)
- Run cp -R en_US/* ../langBundles 
- Run cd ../langBundles
- Run git apply ../locale.patch
- Review any differences, confirm they're correct 
- Create a new patch file (git diff -p > ../locale.patch)
- Commit your changes