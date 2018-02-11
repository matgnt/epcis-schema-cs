# Keywords
xsd xsd.exe EPCIS cs .net csharp c#

# EPCIS
> "Electronic Product Code Information Services (EPCIS) is a global GS1 Standard for creating and sharing visibility event data, both within and across enterprises, to enable users to gain a shared view of physical or digital objects within a relevant business context."

https://en.wikipedia.org/wiki/EPCIS

## GS1
The GS1 provides the necessary xsd files. With the xsd.exe tool, provided by Microsoft, you can generate the necessary cs files to integrate the types into existing c# projects.

https://www.gs1.org/epcis


## Generate cs file on Windows
```
xsd /c /n:epcis /out:cs .\xsd\EPCglobal-epcis-1_2.xsd .\xsd\EPCglobal.xsd .\xsd\StandardBusinessDocumentHeader.xsd
```

The *xsd* tool can be found in e.g.
```
C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.7.1 Tools\x64
```

The comman generates the cs file into the cs subdirectory from the given xsd files with the given namespace.
EPCglobal.xsd and StandardBusinessDocumentHeader.cs are given because imports are used in EPCglobal-epcis-1_2.xsd.

## Mac / Linux

### Possible errors
The Mac / Linux version might show some errors like this:
```
Error: Wildcard '##other' allows element 'extension', and causes the content model to become ambiguous. A content model must be formed such that during validation of an element information item sequence, the particle contained directly, indirectly or implicitly therein with which to attempt to validate each item in the sequence in turn can be uniquely determined without examining the content or attributes of that item, and without any information about the items in the remainder of the sequence. Wildcard '##other' allows element 'extension', and causes the content model to become ambiguous. A content model must be formed such that during validation of an element information item sequence, the particle contained directly, indirectly or implicitly therein with which to attempt to validate each item in the sequence in turn can be uniquely determined without examining the content or attributes of that item, and without any information about the items in the remainder of the sequence.
```

or this:

```
System.InvalidOperationException: The element 'http://www.unece.org/cefact/namespaces/StandardBusinessDocumentHeader:ScopeInformation' is missing.
```

```
System.InvalidOperationException: The datatype 'urn:epcglobal:xsd:1:Document' is missing.
```

The missing datatypes errors are due to xsd imports in the main file. You have to provide all imported files on the command line.

### Generate code with MonoXSD

Beware, that the order of command line arguments is slightly different for `MonoXSD`:
```
xsd ./EPCglobal-epcis-1_2.xsd ./EPCglobal.xsd ./StandardBusinessDocumentHeader.xsd /c
```

## Summary
To make it all easier, we have setup this repostiroy to easily integrate the generated code into your project.
