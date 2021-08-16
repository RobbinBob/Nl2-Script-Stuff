The plan is to replicate javas dom classes into nl2, that way parsing xml files will be easier.
ofc they dont need to be exactly the same, but enough to work

So far the DocumentBuilder and some Schema/Document classes are working, the rest are to be
implemented once the DocumentBuilder can start to sort and arrange each part of the file.

from my understanding:
  Document - contains all information about the file (is the root node)
    NodeList - contains a list of all the nodes(tags : <example></example>)
      Node - a single node within the NodeList

text node refers to text within a node:**

attr node refers to an attribute within a node, a | will always preceed a attribute to signal its presence :
<example | attr="text"/>

element node is the main node type and will hold attr, text :
<example>
  <node1></node1>
  <node2 | attr="text"/>
</example>

every node *except document n a few others* are element nodes, element nodes contain attr nodes and text nodes
from what is documented, it looks as if the element node is first, and then each attr/text node preceeds it
then is closed off with another element node. but i could be wrong, i think to keep things more straight
forward. im going to create a element node, then insert the attr/text/other nodes into the element node
almost as if its some sort of container for the nodes, they will be inserted in the same order they are
found in the xml file, so keeping the order correct will be crucial, especially for things such as switch
tracks which have switch nodes to represent the switch positions.


list of node types and node values

1 - Element : nodeName; element name
2 - Attr :    nodeName; attribute name
3 - Text :    nodeName; #text**
4 - CDATASection - Not used
5 - EntityReference - Not used
6 - Entity - Not used
7 - ProcessingInstruction - Not used
8 - Comment - Not used but could be implemented
9 - Document : nodeName; #document
10 - DocumentType - Not used
11 - DocumentFragment - Not used
12 - Notation - Not used

**Text Nodes
The system implemented for parsing xml files currently does not support the use of text nodes out of the box,
including a text node within the original xml file will cause a fatal error that it can't recover from. This
however can be avoided by inserting the Text via another script after building the Document.