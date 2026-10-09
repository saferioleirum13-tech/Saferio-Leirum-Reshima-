 

Hot Reload
Hot Reload allows a developer to apply changes to the Flutter application's source code while the application is running without completely restarting the application. It normally preserves the current application state. It is useful when making small UI or code changes and you want to see the result immediately.
For example, if you change the color, text, spacing, or layout of a widget, Hot Reload lets you see the change quickly without starting the application again.
Hot Restart
Hot Restart completely restarts the Flutter application and rebuilds its state from the beginning. Unlike Hot Reload, the current application state is lost. Hot Restart is useful when changes affect application initialization, state, or code that Hot Reload cannot properly apply.
Simple difference
Hot Reload	Hot Restart
Keeps current state	Resets application state
Faster	Slower than Hot Reload
Useful for UI/code changes	Useful when a full restart is needed
Does not restart the entire app	Restarts the application
Easy way to remember it:
Hot Reload = change the code and keep your place.
 Hot Restart = start the application again from the beginning.
THE COMMAND ON CMD 
cd /c/src
flutter create my_first_app
cd my_first_app
flutter devices

 
 

 

DELIMITER //

CREATE TRIGGER after_user_insert
AFTER INSERT ON users
FOR EACH ROW
BEGIN
    INSERT INTO audit_log
    (table_name, action_type, record_id, details)
    VALUES
    ('users', 'INSERT', NEW.user_id,
     CONCAT('New user added: ', NEW.full_name));
END//

DELIMITER ;


The audit trigger automatically records every new user added to the system in the audit_log table. This improves accountability and makes it possible to track changes made to the database.

 
Figure: Audit trigger successfully created and displayed in MySQL. 


The audit trigger was tested by adding a new user to the system. The corresponding action was automatically recorded in the audit_log table, confirming that the trigger is working correctly.
 
A database view named enrollment_details was created to simplify access to enrollment information. The view combines users, courses, and enrollments into a single queryable result, making it easier to retrieve and present related information.

 

Soft delete was implemented by adding a deleted_at column to the users table. Instead of permanently removing a user, the system records the deletion time. This preserves the user's information for auditing while allowing the application to display only active users.
 

The EXPLAIN statement was used to examine how MySQL executes an email search. An index on the email column was created to help MySQL locate users efficiently without unnecessarily scanning the entire table.









A JSON column was added to the users table to store flexible profile information such as skills, location, and learning mode. JSON allows related information to be stored in a structured format while remaining flexible for future requirements. A JSON query was also used to retrieve specific values from the stored profile data.

 

 









A separate database user named education_app was created instead of using the root account for normal application operations. The user was granted only the SELECT, INSERT, UPDATE, and DELETE privileges required to work with the community_education database. This follows the principle of least privilege and reduces the risk of unauthorized administrative changes.

 

 

A logical backup of the community_education database was created using MySQL mysqldump. The backup was saved as community_education.sql and can be used to restore the database if the original database is lost or damaged.
 
A successful logical backup of the community_education database was created using MySQL mysqldump. The resulting community_education.sql file was verified and had a size of 9,100 bytes. The backup file contains the database structure and data, including the audit log, courses, enrollments, and users tables.
 
The database backup was restored into a separate test database named community_education_restore. The restored database contained the expected tables, confirming that the backup can be used to recover the database structure and data.
The Community Education Management System database includes relational tables for users, courses, and enrollments; an audit log and trigger for tracking changes; a view for simplified enrollment reporting; soft-delete functionality; JSON profile data; indexing for improved query performance; database access control; and logical backup and recovery procedures.
 
 

The completed database was tested using enrollment reports, active-user queries, audit-log verification, and JSON data retrieval. The tests confirmed that the main database features operate as expected, including relationships between tables, soft deletion, automatic auditing, and flexible JSON data storage.
users.user_id
      ↓
enrollments.user_id

courses.course_id
      ↓
enrollments.course_id
The ER diagram represents the main entities and relationships in the Community Education Management System. Users can enroll in courses through the enrollments table, creating a many-to-many relationship between users and courses through the enrollment records.

