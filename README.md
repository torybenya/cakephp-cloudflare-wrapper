# CloudFlare API plugin for CakePHP 2.0+

This plugin is a (*very*) thin veil over James Ryan Bell's [CloudFlare](https://github.com/jamesryanbell/cloudflare) for use in CakePHP controllers.
Please use composer to install so that the required dependencies are installed.

This was originally forked from https://github.com/Ali1/cakephp-cloudflare-api,
which wrapped a different library that has since been deprecated (it uses Cloudflare's v1 endpoints, and they now require v4.)

## Work in Progress Disclaimer
This work was done for a very specific purpose. Currently it has only been designed and tested to support the Cloudflare\Zone\Cache
functionality available from the other project (see [documentation](https://jamesryanbell.github.io/cloudflare/class-Cloudflare.Zone.Cache.html)).

**It is also likely this functionality will never be extended.** If you need more functionality, please fork this repo and either
create your own version, or submit a pull request to this one :).

## Composer Installation
* Add to composer (run from command line, inside your box)

        "composer require torybenya/cakephp-cloudflare-api"

* Add to composer, this will also install the Amazon SDK for PHP as a dependency

        "torybenya/cakephp-cloudflare-api": "dev-master"

## Non-composer Installation

*  Not supported

## Configuration

* You must add configuration to bootstrap.php. (These keys were kept as CloudflareApi, even though
the new component is simply called Cloudflare, for backwards compatibility.)

		Configure::write('CloudFlareApi.email', 'CLOUDFLARE EMAIL');
		Configure::write('CloudFlareApi.apiKey', 'CLOUDFLARE API KEY');

  *  Don't forget to replace the placeholder text with your actual keys!

* Add the component to a controller

		public $components = array('CloudFlareApi.CloudFlareApi');

## Example

* Remove a file from the cache

		$this->CloudFlareApi->zone_file_purge('mydomain.com', 'http://forum.mydomain.com/images/logo.png');

* From a model or shell

		if (!isset($this->CloudFlareApi)) {
			App::import('Component', 'CloudFlareApi.CloudFlareApi');
			$collection = new ComponentCollection();
			$Controller =& new Controller();
			$this->CloudFlareApi = new CloudFlareApiComponent($collection);
			$this->CloudFlareApi->initialize($Controller);
		}
		$this->CloudFlareApi->zone_file_purge('mydomain.com', 'http://forum.mydomain.com/images/logo.png');

## Notes

You can find the method definitions here: https://jamesryanbell.github.io/cloudflare/

