<a href="https://travis-ci.org/CatalystIT-AU/moodle-auth_saml2">
<img src="https://travis-ci.org/CatalystIT-AU/moodle-auth_saml2.svg?branch=master">
</a>

100% Moodle SAML fast, simple, secure
=====================================

![Churchill quote](/pix/churchill.jpg?raw=true)

* [What is this?](#what-is-this)
* [Why is it better?](#why-is-it-better)
* [How does it work?](#how-does-it-work)
* [Features](#features)
* [Installation](#installation)
* [Testing](#testing)
* [Other SAML plugins](#other-saml-plugins)
* [Warm thanks](#warm-thanks)

What is this?
-------------

This plugin does authentication, user auto creation with field mapping.


Why is it better?
-----------------

* 100% configured in the Moodle GUI - no installation of a whole separate app,
  and no touching of config files or generating certificates.
* Minimal configuration needed, in most cases just copy the IdP metadata in
  and then give the SP metadata to your IdP admin and that's it.
* Fast! - 3 redirects instead of 7
* Supports back channel Single Logout which most big organisations require (unlike OneLogin)


How does it work?
-----------------

It completely embeds a SimpleSamlPHP instance as an internal dependancy which
is dynamically configured the way it should be and inherits almost all of it's
configuration from Moodle configuration. In the future we should be able to
swap to a different internal SAML implementation and the plugin GUI shouldn't
need to change at all.


Features
--------

* Dual login VS forced login for all as an option, with ?saml=off on the login
  page for manual accounts, and ?saml=on supported everywhere to deep link and
  force login via saml if dual auth is on.
* SAML attributes to Moodle user field mapping
* Automatic certificate creation
* Optionally auto create users

Features not yet implemented:

* Enrolment - this should be an enrol plugin and not in an auth plugin
* Role mapping - not yet implemented


Installation
------------

1) Install the plugin the same as any standard moodle plugin either via the
Moodle plugin directory, or you can use git to clone it into your source:

 git clone git@github.com:CatalystIT-AU/moodle-auth_saml2.git auth/saml2

2) Then run the Moodle upgrade
3) If your IdP has a publicly available XML descriptor, copy this url into
   the SAML2 auth config settings page
4) If your IdP requires whitelisting each SP then in the settings page is
   links to download the XML, or you can provide that url to your IdP
   administrator.

For most simple setups this is enough to get authentication working, there are
many more settings to define how to handle new accounts, dual authentication,
and to easily debug the plugin if things are not working.

If you have issues please log them in github here:

https://github.com/CatalystIT-AU/moodle-auth_saml2/issues

Or if you want paid support please contact Catalyst IT Australia:

https://www.catalyst-au.net/contact-us


Testing
-------

This plugin has been tested against:

* SimpleSamlPHP set up as an IdP
* openidp.feide.no
* testshib.org
* An AAF instance of Shibboleth


Other SAML plugins
------------------

The diversity and variable quality and features of SAML moodle plugins is a
reflection of a great need for a solid SAML plugin, but the neglect to do
it properly in core. SAML2 is by far the most robust and supported protocol
across the internet and should be fully integrated into moodle core as both
a Service Provider and as an Identity Provider, and without any external
dependencies to manage.

Here is a quick run down of the alternatives:

**Core:**

* /auth/shibboleth - This requires a separately installed and configured
  Shibbolleth install

One big issue with this, and the category below, is as there is a whole extra
application between moodle and the IdP, so the login and logout processes have
more latency due to extra redirects. Latency on potentially slow mobile
networks is by far the biggest bottle neck for login speed and the biggest
complaint by end users in our experience.

**Plugins that require SimpleSamlPHP**

These are all forks of each other, and unfortunately have diverged quite early
or have no common git history making it difficult to cross port features or
fixes between them.

* https://moodle.org/plugins/view/auth_saml

* https://moodle.org/plugins/view/auth_zilink_saml

* https://github.com/piersharding/moodle-auth_saml

**Plugins which embed a SAML client lib:**

These are generally much easier to manage and configure as they are standalone.

* https://moodle.org/plugins/view/auth_onelogin_saml - This one uses it's own
  embedded saml library which is great and promising, however it doesn't support
  'back channel logout' which is critical for security in any large organisation.

* This plugin, with an embedded and dynamically configured SimpleSamlPHP
  instance under the hood


Warm thanks
-----------

Thanks to the various authors and contributors to the other plugins above.

Thanks to LaTrobe university in Melbourne for sponsoring the initial creation
of this plugin:

http://www.latrobe.edu.au

![LaTrobe](/pix/latrobe.png?raw=true)

Thanks to Centre de gestion informatique de l’éducation in Luxembourg for
sponsoring the user autocreation and field mapping work:

http://www.cgie.lu

![CGIE](/pix/cgie.png?raw=true)

This plugin was developed by Catalyst IT Australia:

https://www.catalyst-au.net/

<img alt="Catalyst IT" src="https://cdn.rawgit.com/CatalystIT-AU/moodle-auth_saml2/master/pix/catalyst-logo.svg" width="400">

