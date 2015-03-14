

# Introduction #

GWT Query-ui is a plugin for GWT Query that enables the use of jQuery-ui widgets. This guide assumes that you are already familiar with GWT Query. If not, please read their [guide](http://code.google.com/p/gwtquery/wiki/GettingStarted) first.

# Setting up a project #

## Using Maven ##

First, add a new repository to your POM file:

```
  <repositories>
    <repository>
      <id>gwtquery-ui-repository</id>
      <url>http://gwtquery-ui.googlecode.com/svn/mavenrepo</url>
    </repository>
  </repositories>
```

Then, add the following dependency:

```
  <dependencies>
    <dependency>
      <groupId>com.google.gwt</groupId>
      <artifactId>gwtquery-ui</artifactId>
      <version>r146</version>
      <scope>provided</scope>
    </dependency>
  </dependencies>
```

Please note that at of this writing, the only available version of gwtquery-ui is [r146](https://code.google.com/p/gwtquery-ui/source/detail?r=146). Look [here](http://gwtquery-ui.googlecode.com/svn/mavenrepo/com/google/gwt/gwtquery-ui/) to see if more recent version(s) exist.

## Using another build tool ##

Directly download the Jar file from the maven repository [here](http://gwtquery-ui.googlecode.com/svn/mavenrepo/com/google/gwt/gwtquery-ui/) and configure your build tool accordingly.

## Configure your GWT module ##

Your GWT module must inherit from the plugin in order to use it. Add the following line to your GWT module descriptor (Module.gwt.xml):

```
  <inherits name='gwtquery.plugins.UiEmbedded' />
```

This will also inject jQuery and jQuery-ui libraries into the host page. See below for more control on how to inject these libraries.

# Using the plugin #

To use any widget or interaction, you must obtain an instance of the gwtquery.plugins.ui.Ui class. This is done through the plugin system of GWT Query.

First, define a static import for the plugin instance:

```
import static gwtquery.plugins.ui.Ui.Ui;
```

Then, from any GQuery instance, obtain an instance of the Ui class:

```
  $("button").as(Ui).button();
```

Please refer to the [samples](http://gwtquery-ui.googlecode.com/svn/demos/GwtQueryUi.html) for a more complete set of examples. Java source is available for each demo, simply expand the "View Source" widget in the sample's page.

# jQuery-ui JavaScript dependency #

This plugin has a dependency on jQuery and jQuery-ui JavaScript libraries. GWT Query-ui can help you add these dependencies to your project. You can choose to:
# add them as static resources provided by the plugin
# add them using a "Content Delivery Network" (either Google or Microsoft CDN)

## Using static resources ##

To load the libraries as static resources (part of your application's resources) you must inherit from `UiEmbedded`:

```
  <inherits name='gwtquery.plugins.UiEmbedded' />
```

This will add the javascript libraries in the public resources of your module and inject them into the `<head>` node of the host page.

## Using Google's CDN ##

To use [Google's CDN](http://code.google.com/apis/libraries/), simply inherit from `UiGoogleCdn`:

```
  <inherits name='gwtquery.plugins.UiGoogleCdn' />
```

This will add two `<script>` nodes to the `<head>` node of the host page pointing to Google CDN.

## Using Microsoft's CDN ##

To use [Microsoft's CDN](http://www.asp.net/ajaxlibrary/cdn.ashx), simply inherit from `UiMicrosoftCdn`:

```
  <inherits name='gwtquery.plugins.UiMicrosoftCdn' />
```

This will add two `<script>` nodes to the `<head>` node of the host page pointing to Microsoft CDN.


## Manual Setup ##

If you already have these libraries installed or don't want this plugin to interfere with your `<head>` node, that's ok to. The plugin will simply "expect" that jQuery and jQuery-ui have been loaded.

```
  <inherits name='gwtquery.plugins.Ui' />
```