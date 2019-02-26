Don't mess with the config. The designers of the database have a much better understanding of their database than you do, any tuning you attempt will only slow things down!

Stored procedures are high performance

Stored procedures enable you to run logic on the server, negating the need to do data transfer back to your api. Therefore the best way to improve performance is to put everything in stored procedures! As an added bonus, SPs can't be unit tested, so you're removing a tonne of work testing!

Views: Views ensure your database is high security. Every table should have an identical view so that your customer can never know your table names.