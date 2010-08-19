cronwrap
===========================================

A cron job wrapper that wraps jobs and enables better error reporting and command timeouts.

Example
===========

Basic example of usage::

    ##Will print out help
    $ cronwrap -h

        usage: cronwrap [-h] [-c CMD] [-e EMAILS] [-t TIME] [-v [VERBOSE]]

        A cron job wrapper that wraps jobs and enables better error reporting and command timeouts.

        optional arguments:
          -h, --help            show this help message and exit
          -c CMD, --cmd CMD     Run a command. Could be `cronwrap -c "ls -la"`.
          -e EMAILS, --emails EMAILS
                                Email following users if the command crashes or
                                exceeds timeout. Could be `cronwrap -e
                                "johndoe@mail.com, marcy@mail.com"`. Uses system's
                                `mail` to send emails. If no command (cmd) is set a
                                test email is sent.
          -t TIME, --time TIME  Set the maxium running time.If this time is passed an
                                alert email will be sent.The command will keep running
                                even if maxium running time is exceeded.The default is
                                1 hour `-t 1h`. Possible values include: `-t 2h`,`-t
                                2m`, `-t 30s`.
          -v [VERBOSE], --verbose [VERBOSE]
                                Will send an email / print to stdout on successful run.


    ##Will send out a timeout alert to cron@my_domain.com:
    $ cronwrap -c "sleep 2" -t "1s" -e cron@my_domain.com

    ##Will send out an error alert to cron@my_domain.com:
    $ cronwrap -c "blah" -e cron@my_domain.com

    #Will not send any reports:
    $ cronwrap -c "ls" -e cron@my_domain.com

    #Will send a successful report to cron@my_domain.com:
    $ cronwrap -c "ls" -e cron@my_domain.com -v
