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

## Locale files
Many display strings are managed in the Dataverse's locale files. See upstream [Internationalization](https://guides.dataverse.org/en/latest/installation/config.html#internationalization) documentation.

- Run mkdir /tmp/languages
- Run cp -R locale/*.properties /tmp/languages
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