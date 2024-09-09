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


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tree Structure</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div id="tree-container"></div>
    <script src="script.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
}

#tree-container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: 50px;
}

.node {
    position: relative;
    text-align: center;
    margin: 10px;
}

.node img {
    border-radius: 50%;
    width: 50px;
    height: 50px;
}

.node-circle {
    border-radius: 50%;
    padding: 20px;
    display: inline-block;
    margin: 10px;
}

.node-blue {
    background-color: blue;
}

.node-silver {
    background-color: silver;
}

.node-gold {
    background-color: yellow;
}

.line {
    position: absolute;
    width: 2px;
    background-color: black;
    transform-origin: top;
}
const data = [
    { id: 1, name: 'Parent 1', certification: 'gold', imgSrc: 'parent1.png' },
    { id: 2, name: 'Parent 2', certification: 'silver', imgSrc: 'parent2.png' },
    { id: 3, name: 'Child 1', certification: 'blue', imgSrc: 'child1.png', parents: [1, 2] },
    { id: 4, name: 'Child 2', certification: 'blue', imgSrc: 'child2.png', parents: [1] }
];

const treeContainer = document.getElementById('tree-container');

function createNode(node) {
    const nodeDiv = document.createElement('div');
    nodeDiv.classList.add('node');

    const circleDiv = document.createElement('div');
    circleDiv.classList.add('node-circle', `node-${node.certification}`);

    const img = document.createElement('img');
    img.src = node.imgSrc;
    circleDiv.appendChild(img);

    nodeDiv.appendChild(circleDiv);
    return nodeDiv;
}

function drawLine(parentNode, childNode) {
    const parentRect = parentNode.getBoundingClientRect();
    const childRect = childNode.getBoundingClientRect();

    const line = document.createElement('div');
    line.classList.add('line');

    const length = Math.sqrt(Math.pow(childRect.left - parentRect.left, 2) + Math.pow(childRect.top - parentRect.top, 2));
    line.style.height = `${length}px`;

    const angle = Math.atan2(childRect.top - parentRect.top, childRect.left - parentRect.left) * (180 / Math.PI);
    line.style.transform = `rotate(${angle}deg)`;

    parentNode.appendChild(line);
}

data.forEach(node => {
    const nodeDiv = createNode(node);
    treeContainer.appendChild(nodeDiv);

    if (node.parents) {
        node.parents.forEach(parentId => {
            const parentNode = document.querySelector(`#tree-container .node:nth-child(${parentId}) .node-circle`);
            drawLine(parentNode, nodeDiv.querySelector('.node-circle'));
        });
    }
});




const data = [
    { id: 1, name: 'Parent 1', certification: 'gold', imgSrc: 'images/parent1.png' },
    { id: 2, name: 'Parent 2', certification: 'silver', imgSrc: 'images/parent2.png' },
    { id: 3, name: 'Child 1', certification: 'blue', imgSrc: 'images/child1.png', parents: [1, 2] },
    { id: 4, name: 'Child 2', certification: 'blue', imgSrc: 'images/child2.png', parents: [1] }
];

const parentContainer = document.getElementById('parent-container');
const childContainer = document.getElementById('child-container');

function createNode(node, container) {
    const nodeDiv = document.createElement('div');
    nodeDiv.classList.add('node');
    nodeDiv.setAttribute('id', `node-${node.id}`);

    const circleDiv = document.createElement('div');
    circleDiv.classList.add('node-circle', `node-${node.certification}`);

    const img = document.createElement('img');
    img.src = node.imgSrc;
    img.alt = node.name;
    circleDiv.appendChild(img);

    nodeDiv.appendChild(circleDiv);
    container.appendChild(nodeDiv);

    return nodeDiv;
}

// Create parent nodes
data.forEach(node => {
    if (!node.parents) {
        const parentNode = createNode(node, parentContainer);
        parentNode.addEventListener('click', () => {
            childContainer.innerHTML = ''; // Clear previous children
            childContainer.style.display = 'flex'; // Show the child container

            // Find and display children
            let hasChildren = false;
            data.forEach(childNode => {
                if (childNode.parents && childNode.parents.includes(node.id)) {
                    createNode(childNode, childContainer);
                    hasChildren = true;
                }
            });

            if (!hasChildren) {
                childContainer.style.display = 'none'; // Hide the container if no children are found
            }
        });
    }
});





const data = [
    { id: 1, name: 'Parent 1', certification: 'gold', imgSrc: 'images/parent1.png' },
    { id: 2, name: 'Parent 2', certification: 'silver', imgSrc: 'images/parent2.png' },
    { id: 3, name: 'Child 1', certification: 'blue', imgSrc: 'images/child1.png', parents: [1, 2] },
    { id: 4, name: 'Child 2', certification: 'blue', imgSrc: 'images/child2.png', parents: [1] }
];

const parentContainer = document.getElementById('parent-container');
const childContainer = document.getElementById('child-container');

function createNode(node, container) {
    const nodeDiv = document.createElement('div');
    nodeDiv.classList.add('node');
    nodeDiv.setAttribute('id', `node-${node.id}`);

    const circleDiv = document.createElement('div');
    circleDiv.classList.add('node-circle', `node-${node.certification}`);

    const img = document.createElement('img');
    img.src = node.imgSrc;
    img.alt = node.name;
    circleDiv.appendChild(img);

    nodeDiv.appendChild(circleDiv);
    container.appendChild(nodeDiv);

    return nodeDiv;
}

function drawLine(parentNode, childNode) {
    const parentRect = parentNode.getBoundingClientRect();
    const childRect = childNode.getBoundingClientRect();

    const x1 = parentRect.left + parentRect.width / 2;
    const y1 = parentRect.top + parentRect.height / 2;
    const x2 = childRect.left + childRect.width / 2;
    const y2 = childRect.top + childRect.height / 2;

    const line = document.createElement('div');
    line.classList.add('line');

    const length = Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2));
    line.style.height = `${length}px`;

    const angle = Math.atan2(y2 - y1, x2 - x1) * (180 / Math.PI);
    line.style.transform = `rotate(${angle}deg)`;
    line.style.transformOrigin = '0 0';
    line.style.position = 'absolute';
    line.style.top = `${y1}px`;
    line.style.left = `${x1}px`;
    line.style.backgroundColor = 'black'; // Line color
    line.style.width = '2px'; // Line thickness

    document.body.appendChild(line);
}

// Create parent nodes
data.forEach(node => {
    if (!node.parents) {
        const parentNode = createNode(node, parentContainer);
        parentNode.addEventListener('click', () => {
            childContainer.innerHTML = ''; // Clear previous children
            childContainer.style.display = 'flex'; // Show the child container

            // Find and display children
            let hasChildren = false;
            data.forEach(childNode => {
                if (childNode.parents && childNode.parents.includes(node.id)) {
                    const childElement = createNode(childNode, childContainer);
                    drawLine(parentNode.querySelector('.node-circle'), childElement.querySelector('.node-circle'));
                    hasChildren = true;
                }
            });

            if (!hasChildren) {
                childContainer.style.display = 'none'; // Hide the container if no children are found
            }
        });
    }
});





const data = [
    { id: 1, name: 'Parent 1', certification: 'gold', imgSrc: 'images/parent1.png' },
    { id: 2, name: 'Parent 2', certification: 'silver', imgSrc: 'images/parent2.png' },
    { id: 3, name: 'Child 1', certification: 'blue', imgSrc: 'images/child1.png', parents: [1, 2] },
    { id: 4, name: 'Child 2', certification: 'blue', imgSrc: 'images/child2.png', parents: [1] },
    { id: 5, name: 'Grandchild 1', certification: 'gold', imgSrc: 'images/grandchild1.png', parents: [3] },
    { id: 6, name: 'Grandchild 2', certification: 'silver', imgSrc: 'images/grandchild2.png', parents: [4] }
];

const mainContainer = document.getElementById('main-container');
const childContainer = document.getElementById('child-container');

function createNode(node, container) {
    const nodeDiv = document.createElement('div');
    nodeDiv.classList.add('node');
    nodeDiv.setAttribute('id', `node-${node.id}`);

    const circleDiv = document.createElement('div');
    circleDiv.classList.add('node-circle', `node-${node.certification}`);

    const img = document.createElement('img');
    img.src = node.imgSrc;
    img.alt = node.name;
    circleDiv.appendChild(img);

    nodeDiv.appendChild(circleDiv);
    container.appendChild(nodeDiv);

    return nodeDiv;
}

function drawLine(parentNode, childNode) {
    const parentRect = parentNode.getBoundingClientRect();
    const childRect = childNode.getBoundingClientRect();

    const parentCenterX = parentRect.left + parentRect.width / 2;
    const parentCenterY = parentRect.top + parentRect.height / 2;
    const childCenterX = childRect.left + childRect.width / 2;
    const childCenterY = childRect.top + childRect.height / 2;

    const line = document.createElement('div');
    line.classList.add('line');

    const length = Math.sqrt(Math.pow(childCenterX - parentCenterX, 2) + Math.pow(childCenterY - parentCenterY, 2));
    line.style.height = `${length}px`;
    line.style.width = '2px'; // Line thickness

    const angle = Math.atan2(childCenterY - parentCenterY, childCenterX - parentCenterX) * (180 / Math.PI);
    line.style.transform = `rotate(${angle}deg)`;
    line.style.transformOrigin = '0 0';
    line.style.top = `${parentCenterY}px`;
    line.style.left = `${parentCenterX}px`;

    document.body.appendChild(line);
}

function clearLines() {
    const lines = document.querySelectorAll('.line');
    lines.forEach(line => line.remove());
}

function removeHighlight() {
    const highlightedNodes = document.querySelectorAll('.node.highlight');
    highlightedNodes.forEach(node => node.classList.remove('highlight'));
}

function displayChildren(parentNode, parentId) {
    childContainer.innerHTML = ''; // Clear previous children
    clearLines(); // Clear previous lines
    childContainer.style.display = 'flex'; // Show the child container

    let hasChildren = false;
    data.forEach(childNode => {
        if (childNode.parents && childNode.parents.includes(parentId)) {
            const childElement = createNode(childNode, childContainer);
            drawLine(parentNode.querySelector('.node-circle'), childElement.querySelector('.node-circle'));
            hasChildren = true;

            childElement.addEventListener('click', () => {
                removeHighlight(); // Remove highlight from previously selected node
                childElement.classList.add('highlight'); // Highlight the clicked child
                displayChildren(childElement, childNode.id); // Recursively display further children
            });
        }
    });

    if (!hasChildren) {
        childContainer.style.display = 'none'; // Hide the container if no children are found
    }
}

// Initialize the main container with top-level nodes (parents)
data.forEach(node => {
    if (!node.parents) { // Top-level parents
        const parentNode = createNode(node, mainContainer);
        parentNode.addEventListener('click', () => {
            removeHighlight(); // Remove highlight from previously selected node
            parentNode.classList.add('highlight'); // Highlight the clicked parent
            displayChildren(parentNode, node.id); // Display children of the clicked parent
        });
    }
});
