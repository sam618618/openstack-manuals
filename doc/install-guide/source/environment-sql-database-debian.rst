Debian SQL database
~~~~~~~~~~~~~~~~~~~

Most OpenStack services use an SQL database to store information. The
database typically runs on the controller node. The procedures in this
guide use MariaDB or MySQL depending on the distribution. OpenStack
services also support other SQL databases including
`PostgreSQL <https://www.postgresql.org/>`__.


Install and configure components
--------------------------------

#. Install the packages:



.. code-block:: console

   # apt install mysql-server python-pymysql

.. end





2. Create and edit the ``/etc/mysql/conf.d/openstack.cnf`` file
   and complete the following actions:

   - Create a ``[mysqld]`` section, and set the ``bind-address``
     key to the management IP address of the controller node to
     enable access by other nodes via the management network. Set
     additional keys to enable useful options and the UTF-8
     character set:

     .. path /etc/mysql/conf.d/openstack.cnf
     .. code-block:: ini

        [mysqld]
        bind-address = 10.0.0.11

        default-storage-engine = innodb
        innodb_file_per_table = on
        max_connections = 4096
        collation-server = utf8_general_ci
        character-set-server = utf8

     .. end




Finalize installation
---------------------


#. Restart the database service:

   .. code-block:: console

      # service mysql restart

   .. end




