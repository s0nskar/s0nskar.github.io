---
layout: post
comments: true
title: NIX in a nutshell
categories: [nix, gsoc17]
permalink: /nix-in-nutshell/
---

<img src="/assets/img/nix_logo.png" alt="NIX logo" width="30%" align="right">
Mentoring Organizations for GSoc'17 announced last week. I decided to contribute to INCF - NIX project this year. NIX DataFrame Support project idea seems interesting to me. As I'm already familiar with Pandas at first, I've got some idea how to implement that. But as soon as I started messing around NIX code it is starting to look a lot overwhelming, and a thought of changing project came into my mind :dizzy_face:. But after hours of banging my head on docs and code few things starting to make sense. I thought it would be better to write a small blog post on my experience explaining NIX :bowtie:. This blog only contains topics that are related to my project in some ways.

### So, What is NIX
NIX (Neuroscience Information Exchange format) in a nutshell defines data models for storing data and metadata for storing in one common format HDF5 (Hierarchical Data Format) in a standard schema predefined by NIX. NIX provide libraries in various languages to conveniently access and visualize the given data. There are other Data Formats for storing the data but due to NIX minimalistic, generic, yet expressive approach it is better from them in one or more ways :+1:. You can download [example.h5](/assets/example.h5) and open it with HDF5 Viewer for a better understanding of how data and metadata are stored in NIX.

### HDF5 ?? Heard it for the first time :confused:
Yup me too!
> HDF5 is a data model, library, and file format for storing and managing data. It supports an unlimited variety of datatypes, and is designed for flexible and efficient I/O and high volume and complex data. HDF5 is portable and is extensible, allowing applications to evolve in their use of HDF5.

The Hierarchical Data Format (HDF5) provides a flexible container that supports groups and datasets, each of which can have attributes. In many ways, HDF5 is similar to a directory structure in a file and, like directory structures, the same data can be structured and annotated in many ways. This flexibility empowers users to arrange information in a manner that make sense to them. So it just a format for storing information in an efficient way :relieved:. You can read more about it on [HDF5 site](https://support.hdfgroup.org/HDF5/whatishdf5.html).

### Data Models
NIX avail various types of data models for storing data. Each of them has `id, name, type and defination`. Further it assumes a central role in the linking between data and metadata. Few types of Data models are breifed below.

+ ##### DataArray:
    DataArray stores data in an n- dimension array along with many physical properties.
+ ##### Tag:
    Tags are used to annotate the data. like events one wants to mark.
+ ##### Feature:
    Feature objects are used to attach further data to Tags than just references into the raw data. like, details of a Tag.
+ ##### Source:
    A Source entity describes the provenance of a DataArray or Tag.
+ ##### Section:
    A Section entity allows linking an Entity to arbitrary metadata described in a Section.
+ ##### Block:
    A Block is the top level grouping element for data objects that somehow are related to each other. It is a requirement, that every data object has to be associated with one Block object.
+ ##### Group:
    The Group establishes subgroups below the Block while entities can be part of multiple Groups. A Group can contain DataArrays, Tags and MultiTags. It further allows linking to Sources and to attach metadata.

Here is an image of various Data Models in NIX, if that helps
<img src="/assets/img/nix_schema.png" alt="Data Models image" width="100%">
For more info visit [NIX Models Defination](https://github.com/G-Node/nix/wiki/Model-Definition).

### Whats Yo Project?
My potential project will be to develop a Proof of Concept for a new Data Model - DataFrame in NIX, and it's bindings for Python, to show that pandas DataFrames can read and write to NIX files.
###### So, What is a DataFrame?
A DataFrame is a table, or two-dimensional array-like Data Structure, in which each column contains potential heterogeneous DataTypes. Each column will have it's own name, unit and data type. Each row data type may be different, while the column datatype must be homogenous. It provides multiple apis for efficient manipulation of data. If want to know more about DataFrame, Pandas DataFrame API's can be a valuable resource.

### But Why DataFrame? :expressionless:
<img src="http://i.giphy.com/1M9fmo1WAFVK0.gif" alt="But why gif" width="90%" align="middle">
Now the question is what is need of DataFrame when there are DataArrays which can store n-dimensional DataTypes.

DataArray can store n-dimensional data with units and other metadata, but the problem with DataArray is that it can only hold only *homogenous* data.
Consider a case in which user wants to store data for an experiment which contains `Int, String and Bool`. To save data user needs to create three different DataArrays and deal with their units and metadata separately. Now consider few more columns with different datatype as the number of columns increases the task of maintaining become quite cumbersome. Using DataFrame makes this a lot easier, leveraging DataFrame API's user can easily store potential heterogeneous data types in one data-structure. And it will be easy to manipulate data, units, and metadata in a systematic way. That's why DataFrame can be a valuable tool in NIX arsenal.

### What Now?
I am currently reading NIX code to get further understanding how various Data Model are implemented deep down. My main interest is in the implementation of DataArray. As DataFrame implemention is gonna be almost similar to them. I will write a new blog post explaing how i am gonna implement POC for DataFrame.

Untill then :wave: