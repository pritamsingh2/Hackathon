# Hackathon

<!DOCTYPE html>
<html>
<head>
	<title>Tree Structure</title>
	<style>
		.tree {
			margin-left: 20px;
		}
		
		.tree ul {
			list-style: none;
			padding: 0;
		}
		
		.tree li {
			margin-bottom: 10px;
		}
		
		.tree li::before {
			content: "";
			border-left: 1px solid #ccc;
			position: absolute;
			left: -20px;
			top: 0;
			bottom: 0;
		}
		
		.tree li:first-child::before {
			top: 20px;
		}
		
		.tree li:last-child::before {
			bottom: 20px;
		}
	</style>
</head>
<body>
	<div id="tree-container"></div>
	
	<script>
		const apiUrl = '(link unavailable)'; // replace with your API URL
		
		fetch(apiUrl)
			.then(response => response.json())
			.then(data => renderTree(data));
		
		function renderTree(data) {
			const container = document.getElementById('tree-container');
			container.innerHTML = '';
			
			data.forEach(tree => {
				const treeElement = document.createElementNS('(link unavailable)', 'svg');
				treeElement.setAttribute('width', '100%');
				treeElement.setAttribute('height', '100%');
				
				// Create a bigger circle to group the children
				const groupCircle = document.createElementNS('(link unavailable)', 'circle');
				groupCircle.setAttribute('cx', '150');
				groupCircle.setAttribute('cy', '150');
				groupCircle.setAttribute('r', '100');
				groupCircle.setAttribute('fill', 'none');
				groupCircle.setAttribute('stroke', '#000');
				treeElement.appendChild(groupCircle);
				
				// Parent circle
				const parentCircle = document.createElementNS('(link unavailable)', 'circle');
				parentCircle.setAttribute('cx', '50');
				parentCircle.setAttribute('cy', '50');
				parentCircle.setAttribute('r', '40');
				parentCircle.setAttribute('stroke', '#000');
				
				// Set the fill color based on the data
				if (tree.certification === 'certified') {
					parentCircle.setAttribute('fill', '#0000FF'); // blue
				} else if (tree.certification === 'silver') {
					parentCircle.setAttribute('fill', '#C0C0C0'); // silver
				} else if (tree.certification === 'gold') {
					parentCircle.setAttribute('fill', '#FFFF00'); // yellow
				} else {
					parentCircle.setAttribute('fill', '#FFFFFF'); // white
				}
				
				const parentImage = document.createElementNS('(link unavailable)', 'image');
				parentImage.setAttribute('href', tree.image); // replace with your image URL
				parentImage.setAttribute('x', '10');
				parentImage.setAttribute('y', '10');
				parentImage.setAttribute('width', '80');
				parentImage.setAttribute('height', '80');
				parentCircle.appendChild(parentImage);
				treeElement.appendChild(parentCircle);
				
				// Children circles
				tree.children.forEach((child, index) => {
					const childCircle = document.createElementNS('(link unavailable)', 'circle');
					childCircle.setAttribute('cx', '150');
					childCircle.setAttribute('cy', '150' + (index * 50)); // position children vertically
					childCircle.setAttribute('r', '30');
					childCircle.setAttribute('stroke', '#000');
					
					// Set the fill color based on the data
					if (child.certification === 'certified') {
						childCircle.setAttribute('fill', '#0000FF'); // blue
					} else if (child.certification === 'silver') {
						childCircle.setAttribute('fill', '#C0C0C0'); // silver
					} else if (child.certification === 'gold') {
						childCircle.setAttribute('fill', '#FFFF00'); // yellow
					} else {
						childCircle.setAttribute('fill', '#FFFFFF'); // white
					}
					
					const childImage = document.createElementNS('(link unavailable)', 'image');
					childImage.setAttribute('href', child.image); // replace with your image URL
					childImage.setAttribute('x', '10');
					childImage.setAttribute('y', '10');
					childImage.setAttribute('width', '60');
					childImage.setAttribute('height', '60');
					childCircle.appendChild(childImage);
					treeElement.appendChild(childCircle);
				});
				
				container.appendChild(treeElement);
			});
		}
	</script>
</




[
  {
    "certification": "certified",
    "image": "image_url_1",
    "children": [
      {
        "certification": "silver",
        "image": "image_url_2"
      },
      {
        "certification": "gold",
        "image": "image_url_3"
      }
    ]
  },
  {
    "certification": "certified",
    "image": "image_url_4",
    "children": [
      {
        "certification": "certified",
        "image": "image_url_5"
      },
      {
        "certification": "silver",
        "image": "image_url_6"
      }
    ]
  }
]


In this example:

- Each object represents a node in the tree.
- certification can have values like "certified", "silver", "gold", or any other custom value.
- image is the URL of the image to be displayed in the node.
- children is an array of child nodes, with the same structure as the parent node.

Replace the (link unavailable) with your actual API URL or image URLs. This data will be fetched and rendered as a tree structure using the provided HTML and JavaScript code.
