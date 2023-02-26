---
title: SQL Server - Full text indexing of html content
date: 2008-12-29
---
Sorry for the long and boring title, but I wanted to make it easy for
Google to find this post.

If you happen to have a site that is storing **Unicode** (that's bold
because it's important, as you will see later!) HTML content in a SQL
Server database and you want to enable full text indexing there are a
few hoops you have to jump through that aren't obvious.

First of all, you can't store your content as varchar, nvarchar or
text.  The assumption is that the text in those columns is plain text so
the indexer uses a vanilla iFilter instead of the iFilter for HTML.  To
use the HTML iFilter you will need to create a pair of columns.  One
"Document Type" column and another varbinary column to store your
content.  What I did was create a document type column and a persisted
calculated varbinary column that was the column actually indexed (not
the column that the application edits).

In the end I had 3 columns:

1.  [Content] -\> This is the varchar(max) column that my application
    updates
2.  [IndexedContent] -\> This is the varbinary(max) column that is
    indexed
3.  [ContentDocumentType] -\> This is the (obviously) Document Type
    column that tells SQL Server to use the HTML iFilter.

Here is the code to setup full text indexing (let's assume you wanted to
index some content in a CMS):

```sql
EXEC sp_fulltext_catalog @ftcat= 'ContentManagementSystem' , 
     @action= 'Create'
GO

EXEC sp_fulltext_table 'dbo.Entries', 'create', 'ContentManagementSystem', 'PK_Entries_EntryID';
GO

EXEC sp_fulltext_service @action='load_os_resources', @value=1;
GO

ALTER TABLE Entries
    ADD IndexedContent AS (0xFFFE+CONVERT([varbinary](max),[Content],0))
GO

ALTER TABLE Entries
    ADD ContentDocumentType AS 'htm'
GO

EXEC sp_fulltext_column 'dbo.Entries', 'IndexedContent', 'add', 'ContentDocumentType'
GO

EXEC sp_fulltext_table 'dbo.Entries','start_change_tracking';
GO

EXEC sp_fulltext_table 'dbo.Entries','activate';
GO
```

The key part is where you see 0xFFEE.  When you are storing Unicode
content in a varbinary field, the field needs to start with those magic
bits or else the indexer doesn't index the field properly and you will
get ZERO results back.