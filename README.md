## ORACLEDB-EX-04
In this exercise, my goal was to write a small Java application that talks directly to the Oracle database I set up in the previous assignments. The task was to generate some sample data and fill up the BOOK table that I had already created in EX-03.

## Steps Completed
	1.	Prepared Oracle Environment
	•	Reused the Oracle XE instance from EX-02/EX-03.
	•	Confirmed that the BOOK table exists.
	2.	Java Project Setup
	•	Created a Maven/Java project.
	•	Added Oracle JDBC driver (ojdbc11.jar) to the classpath.
	3.	Database Connection via JDBC
Example connection string:

String url = "jdbc:oracle:thin:@localhost:1521/FREEPDB1"; // or XEPDB1 for XE
String user = "system";
String password = "ORACLE";
Connection conn = DriverManager.getConnection(url, user, password);


Insert 100 Random Records:
String sql = "INSERT INTO BOOK (ID, NAME, ISBN) VALUES (?, ?, ?)";
PreparedStatement ps = conn.prepareStatement(sql);

for (int i = 1; i <= 100; i++) {
    ps.setInt(1, i);
    ps.setString(2, "Book_" + i);
    ps.setString(3, "ISBN" + (100000 + i));
    ps.executeUpdate();
}
ps.close();
conn.close();

Verification
	•	Ran SELECT COUNT(*) FROM BOOK; → confirmed 100 rows were inserted.
	•	Verified data in SQL Developer.
 <img width="1417" height="520" alt="Screenshot 2025-09-19 at 13 47 11" src="https://github.com/user-attachments/assets/cf59129a-766b-4dea-a883-a423843136f7" />
 <img width="1512" height="612" alt="Screenshot 2025-09-19 at 13 47 50" src="https://github.com/user-attachments/assets/a1fc9b6a-c962-4a3d-b0c1-bf2bd83a20bd" />
 <img width="1511" height="944" alt="Screenshot 2025-09-19 at 13 48 14" src="https://github.com/user-attachments/assets/4e63e2fa-54da-4385-8448-82f97bded57e" />



