# dataform-helper

This is a starter code template with some useful snippets of code to help you set up your own dataform repo. This should not be used as a direct template itself but as a guide to understanding the basics of a simple dataform project setup.

## Folder Structure

The repo has a simple structure, with a definitions folder and a includes folder. The defitions folder should contain all of your sql code and I would advise you to split this up into sections for when your project grows bigger (i.e views, sources, etc). The includes folder contains any scripts needed for dataform to operate, this could include bespoke js scripts/tests for your tables.

The dataform.json file determines the default settings for your project and unless overwritten at runtime, will be the default settings for all dataform pipeline runs.

package.json defines the dataform version being used by the pipeline

## SQLX files

Browse the repo to see how the setup is for different files. See the example below for standard setup:

```
config {
    type: "table",
    tags: ["tag"],
    assertions: {
        uniqueKey: ["year", "day", "key"],
        nonNull: ["key"],
        rowConditions: [
            "REGEXP_CONTAINS(year, r'^[0-9]{4}')"
        ],
    },
    description: "This table contains exciting data",
    columns: constants.getSchemaDescriptions({})
}

SELECT 
  year,
  day,
  key
FROM ${ref('table_1')}
```

## Centralising & Automating Dataform Column Descriptions

This is a quick guide which shows you how to centralise your column descriptions so they can be updated/edited in one place. The advantage of this is that you can avoid duplication in column descriptions and ensure the column descriptions across your dataset are identical and do not diverge. Nobody wants to go into a repo and have to edit every tables schema when a change is made.

[click here for more details](docs/dataform_column_descriptions.md)