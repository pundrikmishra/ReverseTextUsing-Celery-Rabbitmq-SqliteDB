pip install celery
pip install sqlalchemy     ### If you use sqliteDB then install this
celery -A main worker --loglevel=info   ### For starting celery worker write this command in this project
################################# MOST IMPORTANT ################################################################
##  If you initialize celery like this:-
##         app = Celery('main', broker='amqp://guest:@localhost:5672//', backend='db+sqlite:///db.sqlite3')
##         ### Then you have to start celery worker as:-
##                celery -A yourfilename.app worker --loglevel=info
##                    i.e In this project:-
##                            celery -A main.app worker --loglevel=info
##                OR
##                celery -A yourfilename worker --loglevel=info
##                    i.e In this project:-
##
##                            celery -A main worker --loglevel=info
##
## And If you initialize celery like this:-
##      celery = Celery('main', broker='amqp://guest:@localhost:5672//', backend='db+sqlite:///db.sqlite3')
##      ### Then you have to start celery worker as:-
##               celery -A yourfilename.celery worker --loglevel=info
##                     i.e In this project:-
##                           celery -A main.celery worker --loglevel=info
##########################################################################################################################
##########################################################################################################################
#               THIS MEANS,THE NAME WE ASSIGN TO CELERY,
#               THAT SAME NAME IS USED TO START CELERY WORKER
#               LIKE:-
#                       celery -A YourFileName.SameName worker --loglevel=info
#
#               YourFileName = name of that file in which your celery app is running
#               SameName  =  THE NAME WE ASSIGN TO CELERY
#
# For example in main.py file:-
#      1)       app = Celery('main', broker='amqp://guest:@localhost:5672//', backend='db+sqlite:///db.sqlite3')
#                       Then to start celery worker:-
#                               celery -A main.app worker --loglevel=info
#                                       OR
#                               celery -A main worker --loglevel=info
#      2)        celery = Celery('main', broker='amqp://guest:@localhost:5672//', backend='db+sqlite:///db.sqlite3')
#                       Then to start celery worker:-
#                               celery -A main.celery worker --loglevel=info
#                                       AND NOT use below command
#                               celery -A main worker --loglevel=info      ### do not use this command due to some reason
##########################################################################################################################
##########################################################################################################################
url:-
     broker='amqp://guest:@localhost:5672//'   ### for rabbitmq
     backend='db+sqlite:///db.sqlite3'         ### Sqlite database as backend
     backend='rpc://'                          ### rabbitmq as backend
     backend='amqp'


open two terminal on 1st terminal type python command and on 2nd terminal start celery worker:-
                open 1st terminal and type command like:-
                                            (venv) python main.py
                                            (venv) python
                                            Python 3.7.4 (default, Nov 10 2011, 15:00:00)
                                            [GCC 9.3.0] on linux
                                            Type "help", "copyright", "credits" or "license" for more information.
                                            >>> from main import reverse
                                            >>> reverse(pundrik)
                                            Traceback (most recent call last):
                                              File "<stdin>", line 1, in <module>
                                            NameError: name 'pundrik' is not defined
                                            >>> reverse('pundrik')
                                            'kirdnup'
                                            >>> reverse('pundrikmishra')
                                            'arhsimkirdnup'
                                            >>> reverse.delay('pundrikmishra')
                                            <AsyncResult: b0967f45-98f2-4247-bf65-30aa3295102b>
                                            >>> reverse.delay('mishra')
                                            <AsyncResult: 44469735-68b9-4a3a-96a9-d9a1d1658b51>
                                            >>> result = reverse.delay('pundrikmishra')
                                            >>> result
                                            <AsyncResult: 0850ac50-3b03-41b0-a32c-228c1e510c66>
                                            >>> result.get
                                            <bound method AsyncResult.get of <AsyncResult: 0850ac50-3b03-41b0-a32c-228c1e510c66>>
                                            >>> result.get()
                                            'arhsimkirdnup'
                                            >>> reverse.delay('mishra')
                                            <AsyncResult: 812e857f-5e05-4b83-8810-fa7bf0d2223a>
                                            >>> reverse.delay('mishra')
                                            <AsyncResult: 5f7996c4-71fd-48b9-a804-1d054fc6ed5c>
                                            >>> reverse.delay('mishra')
                                            <AsyncResult: 729ae44a-38f1-41c9-b151-77c97732994f>
                                            >>>
                                            [1]+  Stopped(SIGTSTP)        python
                                            (venv)

                Open 2nd terminal and type this command:-
                                            (venv) celery -A main worker --loglevel=info

                                            -------------- celery@amit-HP-Notebook v4.4.7 (cliffs)
                                            --- ***** -----
                                            -- ******* ---- Linux-5.4.0-42-generic-x86_64-with-glibc2.2.5 2020-08-30 22:24:55
                                            - *** --- * ---
                                            - ** ---------- [config]
                                            - ** ---------- .> app:         main:0x7feace03f390
                                            - ** ---------- .> transport:   amqp://guest:**@localhost:5672//
                                            - ** ---------- .> results:     sqlite:///db.sqlite3
                                            - *** --- * --- .> concurrency: 4 (prefork)
                                            -- ******* ---- .> task events: OFF (enable -E to monitor tasks in this worker)
                                            --- ***** -----
                                             -------------- [queues]
                                                            .> celery           exchange=celery(direct) key=celery


                                            [tasks]
                                              . main.reverse

                                            [2020-08-30 22:24:55,607: INFO/MainProcess] Connected to amqp://guest:**@127.0.0.1:5672//
                                            [2020-08-30 22:24:55,622: INFO/MainProcess] mingle: searching for neighbors
                                            [2020-08-30 22:24:57,076: INFO/MainProcess] mingle: all alone
                                            [2020-08-30 22:24:57,128: INFO/MainProcess] celery@amit-HP-Notebook ready.
                                            [2020-08-30 22:24:57,129: INFO/MainProcess] Received task: main.reverse[5f7996c4-71fd-48b9-a804-1d054fc6ed5c]
                                            [2020-08-30 22:25:03,601: INFO/ForkPoolWorker-2] Task main.reverse[5f7996c4-71fd-48b9-a804-1d054fc6ed5c] succeeded in 6.366698895000809s: 'arhsim'
                                            [2020-08-30 22:25:07,784: INFO/MainProcess] Received task: main.reverse[729ae44a-38f1-41c9-b151-77c97732994f]
                                            [2020-08-30 22:25:12,964: INFO/ForkPoolWorker-2] Task main.reverse[729ae44a-38f1-41c9-b151-77c97732994f] succeeded in 5.177802489999522s: 'arhsim'
