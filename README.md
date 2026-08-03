we have Assignments 

Task 1) NullPointerException
Explanation : The method had multiple NullPointerException risks. First, the result list was initialized as null, so calling result.add() would fail. Second, dueDate could be null, so invoking before() without a null check would also throw a NullPointerException. I added a null check for dueDate. I also handled the case where the input list or an element inside it could be null to make the method more robust. The business logic remains the same: return only overdue loan accounts that have an outstanding balance greater than zero.
------------------------------------------------------------------------------------------------------------------------------------------
Task 2) ConcurrentModificationException Analysis
Explanation : 1. What is the exact cause of ConcurrentModificationException in Java?
ConcurrentModificationException occurs when a collection (such as an ArrayList)
is structurally modified while it is being iterated using an Iterator or an
enhanced for-loop. The iterator detects that the collection has been modified
and throws this exception.

2. What code pattern at line 142 most likely triggered this error?
The most likely code pattern is modifying the list while iterating over it.

4. Provide the minimal code change (one or two lines) that resolves this safely.
Use the Iterator's remove() method instead of removing elements directly from the list.
------------------------------------------------------------------------------------------------------------------------------------
Task 3) Thread-safety in BankStatementBatchProcessor
Explanation : The problem is that processedCount++ is not thread-safe because it is a read-modify-write operation. Multiple threads can read the same value and overwrite each other’s updates, causing an incorrect count. The correct fix is to replace the int with an AtomicInteger and use incrementAndGet(), which performs the increment atomically and guarantees an accurate count in a multithreaded environment.
------------------------------------------------------------------------------------------------------------------------------------

Task 4) Fix: Connection Leak in ReportDAO
Explanation : The application hangs because database connections are never returned to the connection pool. Each call to fetchMonthlyReport() creates a Connection, PreparedStatement, and ResultSet, but none are closed. Under continuous load, the connection pool becomes exhausted. The fix is to use try-with-resources, which automatically closes the ResultSet, PreparedStatement, and Connection in reverse order, ensuring proper resource management even if an exception is thrown.
---------------------------------------------------------------------------------------------------------------------------------------------------------------------

Task 5) Exception Handling in DocumentValidator
Explanation : Expected validation failures (such as a null document or empty content) are business validation issues, not system errors, so they should be logged at the WARN level and handled gracefully by returning an invalid ValidationResult. Unexpected exceptions should be logged at the ERROR level using SLF4J and rethrown so they are not silently ignored. In batch processing, exceptions should be logged instead of swallowed, allowing processing to continue while preserving diagnostic information. This approach avoids log flooding, prevents NullPointerExceptions, and makes real production issues easier to identify.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
