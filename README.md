# User-Management-System
My Gitup Repository with Eclipse 
                                         Product  Management  System 



Registration page

<html>
<body>
<form action="create-account.jsp" method="post">
<table style='border:2px solid blue;margin:auto;margin-top:30px'>
<tr>
<td style="padding:10px">
	<label style='font-size:25px'>Enter user id</label>
</td>
<td style="padding:10px">
	<input type='text' style='font-size:18px' name='userid' required>
</td>
</tr>
<tr>
<td style="padding:10px">
	<label style='font-size:25px'>Enter password</label>
</td>
<td style="padding:10px">
	<input type='password' style='font-size:18px' name='pass' required>
</td>
</tr>
<tr>
<td style="padding:10px">
	<label style='font-size:25px'>Enter first name</label>
</td>
<td style="padding:10px">
	<input type='text' style='font-size:18px' name='fname' required>
</td>
</tr>
<tr>
<td style="padding:10px">
	<label style='font-size:25px'>Enter last name</label>
</td>
<td style="padding:10px">
	<input type='text' style='font-size:18px' name='lname' required>
</td>
</tr>
<tr>
<td style="padding:10px" colspan="2" align="right">
<button style='font-size:18px;padding:2px 15px;color:white;background-color:blue;border-radius:4px'>Submit</button>
</td>
</tr>
</table>
<div style='text-align: center;margin-top:10px'>
	 <a href='login.jsp' style='font-size:25px'>Login</a>
</div>
</form>
</body>
</html>




      Login 


Login Page

<html>
<body>
<h2 style="text-align: center;"> Login User</h2>
<form action="authenticate-user.jsp" method="post">
<table style='border:2px solid blue;margin:auto;margin-top:30px'>
<tr>
<td style="padding:10px">
	<label style='font-size:25px'>Enter user id</label>
</td>
<td style="padding:10px">
	<input type='text' style='font-size:18px' name='userid' required>
</td>
</tr>
<tr>
<td style="padding:10px">
	<label style='font-size:25px'>Enter password</label>
</td>
<td style="padding:10px">
	<input type='password' style='font-size:18px' name='pass' required>
</td>
</tr>
<tr>
<td style="padding:10px" colspan="2" align="right">
<button style='font-size:18px;padding:2px 15px;color:white;background-color:blue;border-radius:4px'>Submit</button>
</td>
</tr>
</table>
<div style='text-align: center;margin-top:10px'>
	 <a href='registration.jsp' style='font-size:25px'>Create Account</a>
</div>
</form>
</body>
</html>

   
  

Home page

<%@include file="menu.html" %>
<html>
<body>
<div class="dv">
<h1>Welcome to the product management systems</h1>
</div>
</body>
</html>



Insert page

<%@include file="menu.html" %>
<html>
<body>
<form action="save-record.jsp">
<table class="formta">
<tr>
<td class='pad'>Enter product id</td>
<td class='pad'><input type="number" name="pid" class="tb" required></td>
</tr>
<tr>
<td class='pad'>Enter product name</td>
<td class='pad'><input type="text" name="name" class="tb" required></td>
</tr>
<tr>
<td class='pad'>Enter product brand</td>
<td class='pad'>
	<select class="tb" name="brand">
	 <option>Dell</option>
	 <option>HP</option>
	 <option>Acer</option>
	 <option>Apple</option>
	 <option>Logitech</option>
	</select>
</td>
</tr>
<tr>
<td class='pad'>Enter product price</td>
<td class='pad'><input type="number" name="price" class="tb" required></td>
</tr>
<tr>
<td class="pad" colspan="2" align="right">
	<button class="bt">Save Record</button>
</td>
</tr>
</table>
</form>
</body>
</html>

Show List

<%@page import="java.sql.*"%>
<%@include file="menu.html" %>
<%@include file="conn.jsp" %>
<html>
<body>
<%
Statement st=cn.createStatement();
ResultSet rst=st.executeQuery("select * from productinfo");
%>
<table class="resta" border="1">
<tr>
<th>Product id</th>
<th>Product name</th>
<th>Product brand</th>
<th>Product price</th>
</tr>
<%
while(rst.next())
{
	 %>
	 <tr>
	 <td><%=rst.getString(1)%></td>
	 <td><%=rst.getString(2)%></td>
	 <td><%=rst.getString(3)%></td>
	 <td><%=rst.getString(4)%></td>
	 </tr>
	 <%
}
%>
</table>
</body>
</html>






Show-Record Page


<%@page import="java.sql.*"%>
<%@include file="conn.jsp" %>
<html>
<body>
<%
String pid=request.getParameter("pid");
PreparedStatement ps=cn.prepareStatement("select * from productinfo where pid=?");
ps.setString(1,pid);
ResultSet rst=ps.executeQuery();
if(rst.next())
{
	 %>
	 <%@include file="menu.html" %>
	 <form action="update-record.jsp">
	 <table class="resta" border="1">
	 <tr style='background-color:orange;font-size:23px;color:white'>
	 <th colspan="2">Product details</th>
	 </tr>
<tr>
		<th align="left">Product id</th>
		<td><input type='text' value="<%=rst.getString(1)%>" name="pid" readonly="readonly" style="width:100%"></td>
</tr>
<tr>
		<th align="left">Edit product name</th>
		<td><input type='text' value="<%=rst.getString(2)%>" name="name" style="width:100%"></td>
</tr>
<tr>
		<th align="left">Edit product brand</th>
		<td><input type='text' value="<%=rst.getString(3)%>" name="brand" style="width:100%"></td>
</tr>
<tr>
		<th align="left">Edit product price</th>
		<td><input type='text' value="<%=rst.getString(4)%>" name="price" style="width:100%"></td>
</tr>
<tr>
<td colspan="2" align="right">
	<button class='bt'>Update Record</button>
</td>
</tr>
</table>
</form>
	 <% 	
}
else
{
	 %>
	 <jsp:include page="edit.jsp" />
	 <div class='dvv'>
	 <h2 style='color:red'>Product record with id <%=pid%> not found</h2>
	 </div>
	 <%
}
%>
</body>
</html>


Update-record


<%@page import="java.sql.*"%>
<%@include file="menu.html" %>
<%@include file="conn.jsp" %>
<%
PreparedStatement ps=cn.prepareStatement("update productinfo set name=?,brand=?,price=? where pid=?");
ps.setString(1,request.getParameter("name"));
ps.setString(2,request.getParameter("brand"));
ps.setString(3,request.getParameter("price"));
ps.setString(4,request.getParameter("pid"));
ps.executeUpdate();
%>
<html>
<body>
<div class="dv">
<h2 style='color:green'>Product record has been updated successfully</h2>
</div>
</body>
</html>





Delete page

<%@include file="menu.html" %>
<html>
<body>
<form action="delete-record.jsp">
<table class="formta" style='background-color:red;color:white'>
<tr>
<td class='pad'>Enter product id</td>
<td class='pad'><input type="number" name="pid" class="tb" required></td>
<td class="pad" colspan="2" align="right"><button class="bt">delete Record</button></td>
</tr>
</table>
</form>
</body>
</html>

Delete-record

<%@page import="java.sql.*"%>
<%@include file="conn.jsp" %>
<html>
<body>
<jsp:include page="delete.jsp" />
<div class='dvv'>
<%
String pid=request.getParameter("pid");
PreparedStatement ps=cn.prepareStatement("delete from productinfo where pid=?");
ps.setString(1,pid);
int n=ps.executeUpdate();
if(n>=1)
{
	 %>
	 <h2 style='color:green'>Product record with id <%=pid%> has been deleted</h2>
	 <% 	
}
else
{
	 %>
	 <h2 style='color:red'>Product record with id <%=pid%> does not exist</h2>
	 <%
}
%>
</div>
</body>
</html>



Delete Page

<%@include file="menu.html" %>
<html>
<body>
<form action="delete-record.jsp">
<table class="formta" style='background-color:red;color:white'>
<tr>
<td class='pad'>Enter product id</td>
<td class='pad'><input type="number" name="pid" class="tb" required></td>
<td class="pad" colspan="2" align="right"><button class="bt">delete Record</button></td>
</tr>
</table>
</form>
</body>
</html>

Delete-record page

<%@page import="java.sql.*"%>
<%@include file="conn.jsp" %>
<html>
<body>
<jsp:include page="delete.jsp" />
<div class='dvv'>
<%
String pid=request.getParameter("pid");
PreparedStatement ps=cn.prepareStatement("delete from productinfo where pid=?");
ps.setString(1,pid);
int n=ps.executeUpdate();
if(n>=1)
{
	 %>
	 <h2 style='color:green'>Product record with id <%=pid%> has been deleted</h2>
	 <% 	
}
else
{
	 %>
	 <h2 style='color:red'>Product record with id <%=pid%> does not exist</h2>
	 <%
}
%>
</div>
</body>
</html>




       


