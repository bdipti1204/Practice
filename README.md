# Practice
USE [Practice]
GO
/****** Object:  StoredProcedure [dbo].[InsertEmployee]    Script Date: 03-11-2022 18:38:00 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
ALTER PROCEDURE [dbo].[InsertEmployee]
(
 @Empno int,
 @EName varchar(50),
 @job varchar(20),
 @Salary money
)
AS
BEGIN
declare @v_ck int;
declare @flag int;
set @flag=1
while @flag = 1
begin
--checking empno validation
select @v_ck=dbo.empexist(@Empno) 
if @v_ck > 0 
	begin
		print('Emp no is allocated, Please enter new employee number')
		set @flag = 0
		break
	end
else
begin
	print('Emp no is New and Valid')
end
--chceking job validation
if @job = 'MANAGER' or @job = 'SALESMAN' or @job = 'ANALYST'
	print('Its a valid Job');
else
begin
	print('Jab can be either Manager or salesmna or analyst, Please enter new Job')
	set @flag = 0
	break
end
if @Salary < 2000
begin
	print('sal need to be less than 2000, Please enter new Sal')
	set @flag = 0
	break
end
else
	print('Its a valid sal');
print ('Inserting record into emp table')
	declare @i int=1
	INSERT INTO dbo.Emp (empno,ename,job,sal) VALUES (@Empno,@EName	,@job,@Salary)
	set @flag = 0
end;
END;
