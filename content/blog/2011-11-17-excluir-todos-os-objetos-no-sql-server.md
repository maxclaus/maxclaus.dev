+++
title = "Excluir todos os Objetos no SQL Server"
+++

<img class="size-thumbnail wp-image-301 " title="reset" src="/assets/reset-150x150.gif" alt="" width="150" height="150" />

<p>Este artigo é uma referência á um script que salvou tempo e serviço em um projeto atual. No qual precisávamos zerar o banco, mas com o detalhe que não poderíamos excluí-lo e criá-lo novamente.</p>
<p>Sendo assim o que este script faz é excluir todos os objetos nesta ordem:</p>
<div style="margin: 0 20px; padding: 0 20px;">
<ol style="margin: 0 20px; padding: 0 20px; display: block;">
<li>Stored Procedures</li>
<li>Views</li>
<li>Functions</li>
<li>Foreign Keys</li>
<li>Primary Keys</li>
<li>Tables</li>
<li>Indexes</li>
</ol>
</div>
<div><!--more--></div>
<p>[sourcecode language="sql"]</p>
<p>-- Drop all non-system stored procs<br />
DECLARE @name VARCHAR(128)<br />
DECLARE @SQL VARCHAR(254)<br />
SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] = 'P' AND category = 0 ORDER BY [name])<br />
WHILE @name is not null<br />
BEGIN<br />
    SELECT @SQL = 'DROP PROCEDURE [dbo].[' + RTRIM(@name) +']'<br />
    EXEC (@SQL)<br />
    PRINT 'Dropped Procedure: ' + @name<br />
    SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] = 'P' AND category = 0 AND [name] &gt; @name ORDER BY [name])<br />
END<br />
GO</p>
<p>-- Drop all views<br />
DECLARE @name VARCHAR(128)<br />
DECLARE @SQL VARCHAR(254)<br />
SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] = 'V' AND category = 0 ORDER BY [name])<br />
WHILE @name IS NOT NULL<br />
BEGIN<br />
    SELECT @SQL = 'DROP VIEW [dbo].[' + RTRIM(@name) +']'<br />
    EXEC (@SQL)<br />
    PRINT 'Dropped View: ' + @name<br />
    SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] = 'V' AND category = 0 AND [name] &gt; @name ORDER BY [name])<br />
END<br />
GO</p>
<p>-- Drop all functions<br />
DECLARE @name VARCHAR(128)<br />
DECLARE @SQL VARCHAR(254)<br />
SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] IN (N'FN', N'IF', N'TF', N'FS', N'FT') AND category = 0 ORDER BY [name])<br />
WHILE @name IS NOT NULL<br />
BEGIN<br />
    SELECT @SQL = 'DROP FUNCTION [dbo].[' + RTRIM(@name) +']'<br />
    EXEC (@SQL)<br />
    PRINT 'Dropped Function: ' + @name<br />
    SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] IN (N'FN', N'IF', N'TF', N'FS', N'FT') AND category = 0 AND [name] &gt; @name ORDER BY [name])<br />
END<br />
GO</p>
<p>-- Drop all Foreign Key constraints<br />
DECLARE @name VARCHAR(128)<br />
DECLARE @constraint VARCHAR(254)<br />
DECLARE @SQL VARCHAR(254)<br />
SELECT @name = (SELECT TOP 1 TABLE_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'FOREIGN KEY' ORDER BY TABLE_NAME)<br />
WHILE @name is not null<br />
BEGIN<br />
    SELECT @constraint = (SELECT TOP 1 CONSTRAINT_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'FOREIGN KEY' AND TABLE_NAME = @name ORDER BY CONSTRAINT_NAME)<br />
    WHILE @constraint IS NOT NULL<br />
    BEGIN<br />
        SELECT @SQL = 'ALTER TABLE [dbo].[' + RTRIM(@name) +'] DROP CONSTRAINT ' + RTRIM(@constraint)<br />
        EXEC (@SQL)<br />
        PRINT 'Dropped FK Constraint: ' + @constraint + ' on ' + @name<br />
        SELECT @constraint = (SELECT TOP 1 CONSTRAINT_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'FOREIGN KEY' AND CONSTRAINT_NAME &lt;&gt; @constraint AND TABLE_NAME = @name ORDER BY CONSTRAINT_NAME)<br />
    END<br />
SELECT @name = (SELECT TOP 1 TABLE_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'FOREIGN KEY' ORDER BY TABLE_NAME)<br />
END<br />
GO</p>
<p>-- Drop all Primary Key constraints<br />
DECLARE @name VARCHAR(128)<br />
DECLARE @constraint VARCHAR(254)<br />
DECLARE @SQL VARCHAR(254)<br />
SELECT @name = (SELECT TOP 1 TABLE_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'PRIMARY KEY' ORDER BY TABLE_NAME)<br />
WHILE @name IS NOT NULL<br />
BEGIN<br />
    SELECT @constraint = (SELECT TOP 1 CONSTRAINT_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'PRIMARY KEY' AND TABLE_NAME = @name ORDER BY CONSTRAINT_NAME)<br />
    WHILE @constraint is not null<br />
    BEGIN<br />
        SELECT @SQL = 'ALTER TABLE [dbo].[' + RTRIM(@name) +'] DROP CONSTRAINT ' + RTRIM(@constraint)<br />
        EXEC (@SQL)<br />
        PRINT 'Dropped PK Constraint: ' + @constraint + ' on ' + @name<br />
        SELECT @constraint = (SELECT TOP 1 CONSTRAINT_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'PRIMARY KEY' AND CONSTRAINT_NAME &lt;&gt; @constraint AND TABLE_NAME = @name ORDER BY CONSTRAINT_NAME)<br />
    END<br />
SELECT @name = (SELECT TOP 1 TABLE_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'PRIMARY KEY' ORDER BY TABLE_NAME)<br />
END<br />
GO</p>
<p>-- Drop all tables<br />
DECLARE @name VARCHAR(128)<br />
DECLARE @SQL VARCHAR(254)<br />
SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] = 'U' AND category = 0 ORDER BY [name])<br />
WHILE @name IS NOT NULL<br />
BEGIN<br />
    SELECT @SQL = 'DROP TABLE [dbo].[' + RTRIM(@name) +']'<br />
    EXEC (@SQL)<br />
    PRINT 'Dropped Table: ' + @name<br />
SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] = 'U' AND category = 0 AND [name] &gt; @name ORDER BY [name])<br />
END<br />
GO</p>
<p>-- Drop all indexes<br />
declare @RETURN_VALUE int<br />
declare @command1 nvarchar(2000)<br />
set @command1 = 'DECLARE @indexName NVARCHAR(128)'<br />
set @command1 = @command1 + ' DECLARE @dropIndexSql NVARCHAR(4000)'<br />
set @command1 = @command1 + ' DECLARE tableIndexes CURSOR FAST_FORWARD FOR'<br />
set @command1 = @command1 + ' SELECT name FROM sys.indexes'<br />
set @command1 = @command1 + ' WHERE object_id = OBJECT_ID(''?'') AND index_id &gt; 0 AND index_id &lt; 255 AND is_primary_key = 0'<br />
set @command1 = @command1 + ' ORDER BY index_id DESC'<br />
set @command1 = @command1 + ' OPEN tableIndexes FETCH NEXT FROM tableIndexes INTO @indexName'<br />
set @command1 = @command1 + ' WHILE @@fetch_status = 0'<br />
set @command1 = @command1 + ' BEGIN'<br />
set @command1 = @command1 + ' SET @dropIndexSql = N''DROP INDEX ?.['' + @indexName + '']'''<br />
set @command1 = @command1 + ' EXEC sp_executesql @dropIndexSql'<br />
set @command1 = @command1 + ' print @dropIndexSql'<br />
set @command1 = @command1 + ' FETCH NEXT FROM tableIndexes INTO @indexName'<br />
set @command1 = @command1 + ' END'<br />
set @command1 = @command1 + ' CLOSE tableIndexes'<br />
set @command1 = @command1 + ' DEALLOCATE tableIndexes'<br />
Print '-----------------------------------------'<br />
exec @RETURN_VALUE = sp_MSforeachtable @command1=@command1<br />
GO<br />
[/sourcecode]</p>
<p>Segue o link para o post, no qual encontrei este script: <a href="http://paigecsharp.blogspot.com/2008/03/drop-all-objects-in-sql-server-database.html">http://paigecsharp.blogspot.com/2008/03/drop-all-objects-in-sql-server-database.html</a></p>
