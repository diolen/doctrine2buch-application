Talking - Demo application taken from the Doctrine 2 ORM ebook
==============================================================

* English version of the book: [PHP Data Persistence with Doctrine 2 ORM](https://leanpub.com/doctrine2-en)
* German version of the book: [https://leanpub.com/doctrine2](https://leanpub.com/doctrine2)

This application is for demonstration purposes only and should **not** be used in production.

Installation
------------

The following steps are needed to run the application:

* Set up a PHP >= 5.3 runtime environment and configure the doc root to be folder "public"
* Run "php composer.phar install" to fetch and install the libraries used
* Review and adapt the database connection data in /config/doctrine.php
* Import /data/fixture.sql into the database


Important
------------

In Slim 2.3.0 the protected property $templatePath in Slim/View.php was removed. That produces an application error like this:

Undefined property: Slim\LayoutView::$templatesPath
To avoid this, change $this->templatePath in LayoutView.php to $this->templateDirectory (Lines 65 and 68). The fixed method renderLayout:

protected function renderLayout($layout, $yield) {
    $currentTemplate = $this->templatesDirectory;
    $this->setData('yield', $yield);
    $result = $this->render($layout);
    $this->templatesDirectory = $currentTemplate;
    $this->unsetData('yield');

    return $result;
}
