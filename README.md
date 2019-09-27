<h2>Oracle Script for oracle11g</h2>
 <ul>
	<li> DB Connection</li>
  <li>Table Space Creation</li>
  <li>Schema</li>
  <li>Possible Error Solution</li>
</ul>

<h3>DB Connection</h3>
  <p>(<b>open commad promt</b>)</p>
  <pre>
    <code>
      sqlplus / as sysdba
      username: connect / as sysdba
      pass: oracle
    </code>
  </pre>
  <p>OR (<b>open sql-plus</b>)</p>
  <pre>
    <code>
      connect / as sysdba
      pass: oracle
    </code>
  </pre>
  
  <h3>Possible Error Solution</h3>
   <p>(<b>If error occurred: ([ora-01031] insufficient privileges)</b>)</p>
  <b>solution:</b>
  <ul>
		<li>start menu-></li>
      <ul>
        <li>Oracle-OraDb11g_Home1-></li>
          <ul>
		        <li>Administration Assistant for windows->-></li>
              <ul>
                <li>Oracle Managed Objects-></li>
                  <ul>
		                <li>DESKTOP-EDIVCBS-></li>
                      <ul>
                        <li>OS Database Administrators-Computer-> 
                          <ul>
                            <li>right click(Add/Remove..) </li>
                            <li>select domain</li>
                            <li>salekin [pc user name]</li>
                            <li>click 'Add'. Then 'Ok'. That's it.</li>
                          </ul>
                        </li>
                      </ul>
                  </ul>
              </ul>
          </ul>
      </ul>
  </ul>
  <p>(<b>If error occurred: (ORA-12560: TNS:protocol adapter error)</b>)</p>
  <b>solution:</b>
  <p>Start the service named OracleServiceORCL from Task Manager.</p>
      
  <h3>Displaying username, account_status</h3>
  <pre>
    <code>
      SELECT username, account_status FROM dba_users;
    </code>
  </pre>
  
  <h3>Create Table Space</h3>
  <pre>
    <code>
      CREATE TABLESPACE "A_SYSTEM_TBS" DATAFILE
      'C:/app/username/oradata/orcl/A_SYSTEM_TBS.dbf'
      SIZE 100M AUTOEXTEND ON NEXT 100M MAXSIZE 8G
      LOGGING
      ONLINE
      PERMANENT
      EXTENT MANAGEMENT LOCAL AUTOALLOCATE
      BLOCKSIZE 8K
      SEGMENT SPACE MANAGEMENT AUTO
      FLASHBACK ON;
    </code>
  </pre>
  
  <h3>Drop Table Space</h3>
  <pre>
    <code>
      DROP TABLESPACE A_SYSTEM_TBS
      INCLUDING CONTENTS
      CASCADE CONSTRAINTS;
      OR
      Drop tablespace A_SYSTEM_TBS including contents and datafiles; [It'll also delete the allocated physical file.]
    </code>
  </pre>
  
  <h3>Create Schema</h3>
  <pre>
    <code>
      CREATE USER X
      IDENTIFIED BY password
      DEFAULT TABLESPACE A_SYSTEM_TBS
      TEMPORARY TABLESPACE TEMP
      PROFILE DEFAULT
      ACCOUNT UNLOCK;
    </code>
  </pre>
  
  <h3>Drop Schema</h3>
  <pre>
    <code>
      DROP USER X CASCADE;
    </code>
  </pre>
  
  <h3>Show All Schemas in DB</h3>
  <pre>
    <code>
      select username from dba_users;
      OR
      select * from all_users;
    </code>
  </pre>
  
  <h3>Switching to Different Schema</h3>
  <pre>
    <code>
      ALTER SESSION SET CURRENT_SCHEMA = X;
    </code>
  </pre>
  
  <h3>Give All Privileges to a User</h3>
  <pre>
    <code>
      grant all privileges to X identified by password;
    </code>
  </pre>
  
  <h3>Create Table</h3>
  <pre>
    <code>
      create table customer
      (
      	customerid number(20) not null,
   	customername varchar2(100) null
      );
    </code>
  </pre>
  
  <h3>Drop Table</h3>
  <pre>
    <code>
      drop table customer;
    </code>
  </pre>
  
  <h3>Find Out Both Default Tablespaces (Permanent and Temporary)</h3>
  <pre>
    <code>
      SELECT PROPERTY_NAME, PROPERTY_VALUE
      FROM DATABASE_PROPERTIES
      WHERE PROPERTY_NAME IN ('DEFAULT_PERMANENT_TABLESPACE','DEFAULT_TEMP_TABLESPACE');
    </code>
  </pre>
