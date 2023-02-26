---
title: Stupid SQL tricks
date: 2008-11-19
---
Don't ask why I needed this, but here is a SQL function that will
abbreviate a string:


```sql
create function dbo.fnAbbreviate(@source nvarchar(100))
returns nvarchar(100)
begin
    if charindex(' ', @source) = 0
        return @source
    declare @result nvarchar(100)
    declare @i int
    declare @char nvarchar(1)
    
    set @result = ''
    set @i = 0;

    while @i < len(@source)
    begin
        set @char = substring(@source, @i, 1)

        if CONVERT(varbinary, @char) = CONVERT(varbinary, UPPER(@char))
        begin
            set @result = @result + @char
        end

        set @i = @i + 1
    end

    set @result = REPLACE(@result, ' ', '')

    return @result;
end
```
