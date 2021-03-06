[ ![Download](https://api.bintray.com/packages/mariodavid/cuba-components/cuba-component-loggable/images/download.svg) ](https://bintray.com/mariodavid/cuba-components/cuba-component-loggable/_latestVersion)
[![license](https://img.shields.io/badge/license-Apache%20License%202.0-blue.svg?style=flat)](http://www.apache.org/licenses/LICENSE-2.0)
[![Build Status](https://travis-ci.org/mariodavid/cuba-component-loggable.svg?branch=master)](https://travis-ci.org/mariodavid/cuba-component-loggable)
[![Coverage Status](https://coveralls.io/repos/github/mariodavid/cuba-component-loggable/badge.svg)](https://coveralls.io/github/mariodavid/cuba-component-loggable)

# CUBA Platform Component - Loggable

This application component lets you easily add log entries to any entity in your application.


## Installation

1. `loggable` is available in the [CUBA marketplace](https://www.cuba-platform.com/marketplace)
2. Select a version of the add-on which is compatible with the platform version used in your project:

| Platform Version | Add-on Version |
| ---------------- | -------------- |
| 7.2.x            | 0.1.x          |


The latest version is: [ ![Download](https://api.bintray.com/packages/mariodavid/cuba-components/cuba-component-loggable/images/download.svg) ](https://bintray.com/mariodavid/cuba-components/cuba-component-loggable/_latestVersion)

Add custom application component to your project:

* Artifact group: `de.diedavids.cuba.loggable`
* Artifact name: `loggable-global`
* Version: *add-on version*


## Supported DBMS

The following databases are supported by this application component:

* HSQLDB
* PostgreSQL

All other DBMS systems are supported in the way, that CUBA studio automatically creates DDL scripts.
Therefore it is totally possible to use the application component even without dedicated SQL scripts directly from this application component.

## Using the application component

### Browse Screens

Let your browse screens implement the `WithLogEntriesSupport` interface.

```java

public class CustomerBrowse extends StandardLookup<Customer> implements WithLogEntriesSupport {

    @Inject
    protected GroupTable<Customer> customersTable;

    @Inject
    protected ButtonsPanel buttonsPanel;

    @Override
    public ListComponent getListComponentForLogEntries() {
        return customersTable;
    }

    @Override
    public ButtonsPanel getButtonsPanelForLogEntries() {
        return buttonsPanel;
    }

    @Override
    public WindowManager.OpenType logEntryListOpenType() {
        return WindowManager.OpenType.NEW_TAB;
    }
}
```

In the Interface variant the following attributes have to be defined by implementing methods instead of annotation attributes:

* `getListComponentForLogEntries` defines the list component to target for the loggable functionality
* `getButtonsPanelForLogEntries` defines the button panel on which a button will be placed
* `logEntryListOpenType` optionally defines the open type for the logEntry list



### Edit Screens

Besides using LogEntries in the Browse Screen of the Entity, it is also possible to show LogEntries as part of an Edit Screen.

In order to do display logEntries of a particular Entity there is a `fragment` which can be used in the Edit Screen:

```xml
<fragment screen="ddcl_EntityLogEntriesFragment">
    <properties>
        <property name="loggableDc" ref="customerDc"/>
    </properties>
</fragment>
```

An example can be found in the [customer-edit.xml](https://github.com/mariodavid/cuba-example-using-loggable/blob/master/modules/web/src/com/company/ceua/web/customer/customer-edit.xml#L53).

### Example usage
To see this application component in action, check out this example: [cuba-example-using-loggable](https://github.com/mariodavid/cuba-example-using-loggable).