NG Schematics Goal
Reduce coding routine tasks

- scuffold: new component and services
- update code to fix breaking changes
- apply massive changes to a large project

Automated code changes
- fast
- reliable
- configurable

Real use cases

Adding complex component to project

Classical way
- Find example in documentation
- npm install -s @big/component dependencyA dependencyB …
- update Angular modules imports
- copy example code, styles, layout…
- import styles
- …
- …

Repeat on several projects with a little bit different structure?
Oh, no… :(

Schematics way
- Check generator options
- ng generate rj-bolt:grid —name=Awesome —rowModelType=serverSide —enterprise —module=clients ….

Update all rj-bolt imports
Introducing secondary entry points caused update that required numerous simple fixes

Import {Grid, GridCellInterface, Row, List, Image } from ‘library’;

Better bundle size
Better dependencies management
Faster re-compilation

Import { Grid, GridCellInterface } from ‘library/grid’;
Import { List, Row } from ‘library/list’;
Import { Image } from ‘library/image’;

Possible hundreds and thousands of changes…

Classic way
- Oh, no… :(

Schematics
ng update —from=3 —to=4

Goals
Easy of use and development
Extensibility and Reusability
Atomicity
Asynchronicity

How does it work?

Collection
List of available for package schematics
Special names: ng-add / ng-new
Can extend other collection

// screen of package.json with collection.json path

// screen of collection.json

Migrations

// screen of migrations in package.json

Schematic
Name in collection - available
Schema.json (optional)
Rule factory to be called
(options: any) => Rule


Tree
Virtual file system
Contains both original file system content and changes
Works synchronously
Tree.read(file) / .exists(..) / .rename / …
Changes to FS applied at the end all at once

Rule
Function changing the tree
(tree: Tree, context: SchematicContext) => Tree | Observable<Tree> | Rule | void;

Template
/__name__.class.ts
/__name__-__isMobile__.template.html
<% if (x) { %> <content>...</content> <% } %>

Action
Information about any atomic change in tree
Create / Update / Delete / Rename
tree.actions - all changes one by one

Combining them together
Example 1. Empty
// ng new / schematics  blank --name=example-schematic / npm link … / apply
dryRun
dryRun=false

Example 2. Add line to existing file

Example 3. apply(url(), [template(...)])

Example 4. + chain schematic from same repo

Example 5. + chain external schematic

Modifying code
Regular expressions: easy implementation, but error prone
Abstract Syntax Tree: reliable, requires much more effort

// AST viewer screen
// AST code example screen 

Example 6. + create angular component and populate using ast

Debug
Using 'node --inspect-brk + Chrome DevTools'’

// debug example

Coming soon
ng new
ng add
more components / features supported

Documentation site update

Further reading

Thank you!

Contacts
