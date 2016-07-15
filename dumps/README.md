# Database dumps

Database dumps called {{ database_name }}.sql.gz will be

1. Imported into the database {{ database_name }}
2. Moved aside with a suffix .imported

whenever provisioning is done. Once the dump is moved aside, it will
be ignored on any future provisioning i.e. the dump is not imported
twice unless you move it back.
