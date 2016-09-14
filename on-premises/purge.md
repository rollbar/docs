# Purging Data

If your database starts getting too big, you can purge old raw items.

## Backup First

You should run a backup before purging data.  Seriously, you should.  No
matter how much testing we do on the purge script, there's no reasonable
way we can guarantee you it won't run wild and delete all your data.
It's dangerous purging data.  It's also super easy to give the purge
script the wrong date and purge data you didn't mean to.

## Check Your Backups

Next, test your backups, because it's amazing how often backups are
corrupt, incomplete, or just plain broken.  I wish I were kidding.  And
it's usually too late when you find out.

## Purge Data

The `utils.sh` script has an option for purging data. It requires you to
know the project id, project slug, and a unix timestamp for when to
start your purge.  It'll purge all items in that project older than the
timestamp.  Therefore, `utils.sh` also has an option to give you a list
of all your projects and their slugs.

First, get your project information:

```
$ ./utils.sh --proj-list
Running utilities

Listing information for all projects

+----+------------+----------+-------------+
| id | account_id | slug     | description |
+----+------------+----------+-------------+
|  1 |          1 | HProject | HProject    |
+----+------------+----------+-------------+

All desired utilities ran successfully
```

The `id` and `slug` columns are the interesting ones.  Note that you'll
need to run a separate purge for each project.

Next, get the unix timestamp where you want your purge to start.  This
will purge all items the same age or older than the given
timestamp. Start out by getting the current timestamp (which is in
seconds), then subtract the number of seconds back to when you want your
purge to start. Here's how to get the timestamp for the current time.

```
$ date +%s
1473719424
```

Since there are 86,400 seconds in a day, if we wanted to purge
everything one day old or older, we'd calculate this by subtracting
86,400 from the timestamp we got.

```
1473719424 - 86400 = 1473633024
```

Now that you've gotten the project information, you can run the purge on
each project to get rid of all items older than a day.

```
$ ./utils.sh --purge 1:HProject:1473633024
```

## Compact raw_item Table

Currently, you'll need to compact the raw item table by hand.  We don't
have a utility for that yet.  This will be easiest for people who manage
their own databases.  If you use the mysql server included in the
on-prem distribution, you'll need to get some more instructions from us
on how to do that.

```
$ mysql -u root -p mox_raw
mysql> ALTER TABLE raw_item FORCE;
```

This may cause locking issues, depending on which version of myqsl you
are running.  Therefore it's not a bad idea to shut down the system
while you're compacting the raw item table.
