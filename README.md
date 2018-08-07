# inflate-template

This library is responsible for inflating a template with data. 

It provides the 'export' functionality for [Data-Forge Plot](https://www.npmjs.com/package/data-forge-plot) and
[Data-Forge Notebook](http://www.data-forge-notebook.com/).

## Premise

A template is any number of assets (text files, JS files, HTML files, etc) in a directory. Each asset is a Handlebars template that can be expanded by data.

A template can be expanded in memory or expanded and written another directory on disk.

This library is used by Data-Forge Plot and Data-Forge Notebook to expand a data set into a web page, either in memory and then rendered to a PNG or PDF file or then exported to disk as a browser-based visualization.

## Creating a template

A template is a directory that contains template files that will be inflated with data when the template is expanded.

This repository contains an example template under the test-template directory. Please use this to understand the basics of how a template is constructed.

## Programmatic Usage

# Installation

    npm install --save inflate-template

# Require

JavaScript:

    const { inflateTemplate, exportTemplate } = require('inflate-template');

TypeScript:

    import { inflateTemplate, exportTemplate } from 'inflate-template';

# Usage

Expand in memory:

    const data = { /* ... your data to be expanded into the template ... */ }
    const options = {
        templatePath: "<path-to-load-your-template-from>",
    };
    const template = await inflateTemplate(data, options);

    console.log(template.files.length); // Print number of files in the template.

    const fileContent = await template.files[0].expand(); // Expand first files content.

    const outputPath = "<directory-to-export-expanded-template-to>";
    await template.files[0].export(outputPath); // Export first file to output directory.

Expand to disk:

    const data = { /* ... your data to be expanded into the template ... */ }
    const outputPath = "<directory-to-export-expanded-template-to>";
    const options = {
        templatePath: "<path-to-load-your-template-from">,
    };
    await exportTemplate(data, outputPath, options); // All expanded files are written to output directory.

## Command line usage

This can also be used from the command line to test export templates.

Before using from the command line make sure your template contains a 'test-data.json' that is used to fill out the template.

To use from the command line please install globally like this:

    npm install -g inflate-template

You can also omit the `-g` and just install locally, but then make sure you prefix all the subsequent commands with `npx`.

To inflate and export a template:

    inflate-template export --template=<path-to-your-web-page-template> --out="<path-to-output-your-expanded-template>"

You can also add the `--overwrite` argument to overite an existing export.

