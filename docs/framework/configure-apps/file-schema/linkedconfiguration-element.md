---
description: "Learn more about: <linkedConfiguration> element"
title: "<linkedConfiguration> element"
ms.date: "10/23/2023"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/assemblyBinding/linkedConfiguration"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#linkedConfiguration"
helpviewer_keywords: 
  - "configuration files [.NET Framework],linked configuration files"
  - "<linkedConfiguration> element"
  - "including configuration files"
  - "linked configuration files"
  - "linkedConfiguration Element"
ms.assetid: 8eb34f3b-427e-4288-a7ff-c73f489deb45
---

# \<linkedConfiguration> element

Specifies a configuration file to include.

[**\<configuration>**](configuration-element.md)\
&nbsp;&nbsp;[**\<assemblyBinding>**](assemblybinding-element-for-configuration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<linkedConfiguration>**

## Syntax

```xml
<linkedConfiguration href="URL of linked configuration file" />
```

## Attribute

| Attribute | Description |
| --------- | ----------- |
| **href** | Required attribute.<br><br>The URL of the configuration file to include. The only format supported for the **href** attribute is `file://`. Local files and UNC files are supported. |

## Parent element

| Element | Description |
| --- | ----------- |
| [\<assemblyBinding> Element](assemblybinding-element-for-configuration.md) | Specifies assembly binding policy at the configuration level. |

## Child elements

None

## Remarks

The **\<linkedConfiguration>** element simplifies servicing for component assemblies. If one or more applications use an assembly that has a configuration file residing in a well-known location, their configuration files can use the \<linkedConfiguration> element to include the assembly configuration file, rather than duplicating configuration information. When the component assembly is serviced, updating the common configuration file provides updated configuration information to all applications that use the assembly.

> [!NOTE]
> The \<linkedConfiguration> element isn't supported for applications with Windows side-by-side manifests.

The following rules govern the use of linked configuration files:

- The settings in included configuration files only affect loader binding policy and are used only by the loader. The included configuration files can have settings other than binding policies, but those settings don't have any effect.

- The only format supported for the `href` attribute is `file://`. Local files and UNC files are supported.

- There's no constraint on the number of linked configurations per configuration file.

- All linked configuration files are merged to form one assembly configuration file, similar to the behavior of the `#include` directive in C/C++.

- The \<linkedConfiguration> element is allowed only in application configuration files. If the element appears in a *Machine.config* file, it's ignored.

- There's no restriction on the content of the included configuration files, as long as they conform to the schema of the parent \<assemblyBinding> element.

- Circular references are detected and terminated. That is, if the \<linkedConfiguration> elements of a series of configuration files form a loop, the loop is detected and stopped.

## Example

The following example shows how to include configuration file from a local hard drive:

```xml
<configuration>
  <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
    <linkedConfiguration href="file://c:\Program Files\Contoso\sharedConfig.xml"/>
  </assemblyBinding>
</configuration>
```

## See also

- [\<assemblyBinding> Element](assemblybinding-element-for-configuration.md)
- [Configuration file schema for the .NET Framework](index.md)
