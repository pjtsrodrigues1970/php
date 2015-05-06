# php
<!DOCTYPE HTML>
<html>
	<head>
		<title>Review Individual Product Information</title>
		<link rel="stylesheet" type="text/css" href="http://localhost/project/styles/main.css">
	</head>
	<h1>Review Individual Product Information and Enter Quantity</h1>
	<body>
		<form action="reviewInformation.php" method="post">
			<table id="enterProductInformation">
			<?php
				session_start();
				if (isset($_SESSION['customerID']))
				{
					$customerID = $_SESSION['customerID'];
				}
				else
				{
					if (isset($_POST['customerID']))
					{	
						$customerID = $_POST['customerID'];
						
					}
					else
					{
						echo "<p>Enter Customer ID</p>";
						echo "<input name='customerID' type='text'/>";
					}
				}
				echo "Customer ID:   " .$customerID;
				

				
				#var_dump($customerID);				
				#var_dump($sku);
				$conn=mysqli_connect("localhost", "root", "", "class");				
				
				$sql="select * from products;";
				
				$result = mysqli_query($conn, $sql);
				#var_dump($result);
			
				
				$quantity = 0;
				$sku= "";
				$productName = "";
				$price = "";
				while($rec=mysqli_fetch_assoc($result))
				{
					var_dump(isset($_POST[$rec['sku']]));
					if (isset($_POST[$rec['sku']]))
					{
						//var_dump($rec['sku']);
						
						echo "<tr><th>SKU</th><td>";
						
						echo $rec['sku'] . "</td><tr>";
						echo "<tr><th>Product Name</th><td>" .$rec['name'] ."</td></tr>";
						echo "<tr><th>Price</th><td>" .$rec['price'] ."</td></tr>";
						echo "<tr><th>Enter Product Quantity</th><td><input type='text' name='quantity'></input></td>";
						echo "</tr>";
						$sku = $rec['sku'];
						$productName = $rec['name'];
						$price = $rec['price'];
					}
					
						
				}
				#var_dump($price);
				
			?>
			<input type="hidden" name="customerID" value="<?=$customerID?>"/>
			<input type="hidden" name="sku" value="<?=$sku?>"/>
			<input type="hidden" name="productName" value="<?=$productName?>"/>
			<input type="hidden" name="price" value="<?=$price?>"/>
			</table>
			<input type="submit" id="addToCart" value="Add to Cart" ></input>
		</form>
		<form action="viewProductsAfterCustomer.php" method="post">
			<input type="hidden" name="customerID" value="<?=$customerID?>"/>
			<input type="submit" id="returnToProducts" value="Return to Products"></input>
		</form>
	</body>            
</html>
