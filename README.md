## Notice

This project was originally started by [deltreey][0] and forked by me. Deltreey later deleted his repo causing my fork to become the primary. Since this project effectively fell into my lap, I can only say I will do my best to manage and maintain it. If you have any questions or bugs, please feel free to open an [issue][1].

Dable
=====

Dable (pronounced 'dabble') is a simple javascript table control with filtering, sorting, paging, styles, and more!

Dable is simple and elegant.  It has _zero_ dependencies and works in IE8+.

Initialize a new Dable with

```javascript
var dable = new Dable();
```
Build your Dable by giving it data and column names.

```javascript
var data = [ [ 1, 2 ], [ 3, 4 ] ];
var columns = [ 'Odd', 'Even' ];

dable.SetDataAsRows(data);		// We can import data as rows or columns for flexibility
dable.SetColumnNames(columns);	// Because the data is raw, we need to name our columns
```
If you want to style your Dable, you can use custom styling with easy to remember classes and IDs.
Or you can just select JQueryUI or Bootstrap for preconfigured styles.

```javascript
dable.style = "JqueryUI";	// Don't worry about uppercase/lowercase
```
Dable is pure javascript, so you don't have to add a CSS file to your project.  However, if you use a custom style, make sure you include the relevant stylesheet.

Creating your Dable is as simple as using the id of a div from your page and calling

```javascript
dable.BuildAll(divId);
```
__Everything in Dable is designed to be modifiable by you.__

The Search is an array of callbacks, so you can add your own with a simple command.

```javascript
dable.filters.push(function (searchText, cellValue) {
	//this is a custom filter
});
```
Because it's a simple array, you can wipe out the existing filters altogether if you don't like them.
Your columns are a simple object array.  Each object has a Tag, a FriendlyName, and can be provided with CustomRendering and CustomSortFunc callbacks

```javascript
{ Tag, FriendlyName, CustomSortFunc, CustomRendering }
```
These callbacks are simple to use too.  When you want to render something uniquely, just return the text to render and it'll be stuck in the cell.

```javascript
dable.columnData[0].CustomSortFunc = function (cellValue) {
	return '<a target="_blank" href="/?cell=' + cellValue + '">' + cellValue + '</a>';
}
```
When you want to sort something uniquely, just return an array of the rows to present in whatever order you want.

```javascript
dable.columnData[1].CustomSortFunc = function (columnIndex, ascending, currentRows) {
	return currentRows.reverse();
}
```
What about printing?  If your table is paged, you need to be able to output all the rows to print!
Here's a sample of how to do this extremely complex Dable procedure.

```javascript
dable.pageNumber = 0;				// Go back to the first page
dable.pageSize = dable.rows.length;	// Change the page size to the whole table size
dable.UpdateDisplayedRows();		// Update the table
dable.UpdateStyle();				// Reapply our styles
```

Every function inside of Dable is accessible, down to the initial rendering functions!

[0]: https://github.com/deltreey
[1]: https://github.com/danielkrainas/Dable/issues