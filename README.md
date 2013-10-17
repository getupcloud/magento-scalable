Scalable Magento on GetupCloud
==============================

Magento Store with Scalability.

This git repository creates a Magento installation on OpenShift.

Running on Getupcloud
---------------------

Create an account at http://getupcloud.com/

Create a php-5.5 + mysql-5.1 application, based on this repo's code (you can call your application whatever you want).

    $ rhc app create magento php-5.5 mysql-5.1 http://cartreflect-claytondev.rhcloud.com/reflect?github=smarterclayton/openshift-redis-cart --from-code=git://github.com/getupcloud/magento-scalable.git -s

That's it! You can now access your scalable Magento at [http://magento-$namespace.getup.io/](http://magento-$namespace.getup.io/)
	
Default admin credentials:

    Username: admin
    Password: OpenShiftAdmin123

### Post-installation details

#### Change Secret Key

For security reasons you __must__ change the default secret key.

To generate a new secret key, run:

    $ openssl rand -base64 33
    3LO7wgdZV/4VHPxzgxWOc5IMjBfBXVWH7D3Y6VHl17g3
	
Copy and paste the result inside tag `<key>` of file `php/app/etc/local.xml.erb` on your local repo 
(pay attention to keep `![CDATA[...]]`).
Example:

    <crypt>
       <key><![CDATA[3LO7wgdZV/4VHPxzgxWOc5IMjBfBXVWH7D3Y6VHl17g3]]></key>
    </crypt>
    
Now, commit and push:

    $ git commit -m 'Update secret key' php/app/etc/local.xml.erb
    $ git push

Login to `https://magento-$namespace.getup.io/admin` and change the admin password,
as other Magento configurations.
	
#### Enable Storage Configuration Media

Go to `System` -> `Configuration` -> `Menu Advanced` -> `System`.

Change `Storage Configuration for Media` to `Database`, click on `Synchronize` and then `Save Config`.


### Important!!

Go to `System` and enable all following settings:

* Cache Management
* Index Management
* My Account
* Configuration -> General -> Countries Options
* Configuration -> General -> Locale Options
* Configuration -> Admin
* Configuration -> System
