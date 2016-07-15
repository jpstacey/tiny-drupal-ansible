# Web root

To permit composer-based Drupal installs, both Drupal core (in web/) and
also the composer downloads (in vendor/) need to be present: it's not
enough just to map through the core folder alone.

This is fine in a development environment; in production you'll need to
make sure your vendor/ folder is not directly accessible e.g. on your
server's IP address.
