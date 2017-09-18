<!DOCTYPE>
<html>  
<head>
<style>
.dataform{  
    padding:10px;  
    border:1px solid pink;  
    border-radius:10px;  
    width:300px;
    margin-left:500px;
    margin-top: 100px;
    
}  
.dataform2{  
    padding:10px;  
    border:1px solid pink;  
    border-radius:10px;  
    width:300px;
    margin-left:500px;
    margin-top: 100px;
    }
.formheading{  
    background-color:red;  
    color:white;  
    padding:4px;  
    text-align:center;  
}  
.sub{  
background-color:red;  
padding: 7px 40px 7px 40px;  
color:white;  
font-weight:bold;  
margin-left:70px;  
border-radius:5px;  
}  
table, th, td {
    border: 1px solid black;
}
</style>

</head> 
<body>  
<div class="dataform">  
<h3 class="formheading">A small example page to insert some data in to the MySQL database using PHP</h3>  
<form method="post" action="" >  
<table>  
<tr><td>DATE</td><td><input type="date" name="date"/></td></tr>  
<tr><td>OB</td><td><input type="varchar" name="ob"/></td></tr>
<tr><td>ORE</td><td><input type="varchar" name="ore"/></td></tr>
<tr><td>STOCKPILE</td><td><input type="varchar" name="sp"/></td></tr>  
<tr><td colspan="2" style="text-align:center"><input class="sub" type="submit" value="Add values"/></td></tr>  
</table>  
</form>  
</div> 
<div class="dataform2">
<form method="post" name="display" action="" />
Enter the date you like to display the data from MySQL:<br>
<input type="date" name="date" />
<input type="submit" name="Submit" value="display" />
</form>
</div>


<?php
$servername = "localhost";
$username = "root";
$password = "root";
$dbname = "myDB";

// Create connection
$conn = mysqli_connect($servername, $username, $password, $dbname);
// Check connection
if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}

$sql = "INSERT INTO dashboard (date, ob, ore, stkpl)
VALUES ('$_POST[date]','$_POST[ob]','$_POST[ore]','$_POST[sp]')"; //error here


if (mysqli_query($conn, $sql)) {
    echo "<h1>New record created successfully<h1>";
     
} else {
   // echo "Error: " . $sql . "<br>" . mysqli_error($conn);
}


mysqli_close($conn);

 
?>




<?php
$servername = "localhost";
$username = "root";
$password = "root";
$dbname = "myDB";

$conn = new mysqli($servername, $username, $password, $dbname);
// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
} 
$date = $_POST['date']; //error here
$sql = "select * from dashboard where date = '$date'";
$result = $conn->query($sql);
if ($result->num_rows > 0) {
    // output data of each row
    echo "<h1> your results</h1>";
    echo "<table><tr><th>OB</th><th>ORE</th><th>STOCKPILE</th></tr>";
    while($row = $result->fetch_assoc()) {
    
        echo "<tr><td>".$row["ob"]."</td><td>".$row["ore"]."</td><td>".$row["stkpl"]."</td></tr>" ;
    }
echo"</table>";
} else {
    echo "0 results";
}
$conn->close();

?>


</body>
</html> 
