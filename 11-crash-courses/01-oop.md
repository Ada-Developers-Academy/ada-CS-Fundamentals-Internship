# Object Oriented Programming: A Crash Course

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=05492e44-4ee6-4dad-8f01-af54011f5603&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## OOP Crash Course Slides
- [Slide Deck used for OOP Crash Course](https://docs.google.com/presentation/d/1HYJDxmwykDBH2sSQMdmGPHp33QfrS1bmAOmTOPMWfsc/edit?usp=sharing)

## Python Tutor
- [Linked List Visualization with Python Tutor](https://pythontutor.com/render.html#code=class%20Node%3A%0A%20%20%20%20def%20__init__%28self,%20value%29%3A%0A%20%20%20%20%20%20%20%20self.val%20%3D%20value%0A%20%20%20%20%20%20%20%20self.next%20%3D%20None%0A%0A%20%20%20%20def%20printNode%28self%29%3A%0A%20%20%20%20%20%20%20%20print%28self.val%29%0A%0Aclass%20LinkedList%3A%0A%20%20%20%20def%20__init__%28self,%20head%20%3D%20None%29%3A%0A%20%20%20%20%20%20%20%20self.head%20%3D%20head%0A%0A%20%20%20%20def%20printList%28self%29%3A%0A%20%20%20%20%20%20current%20%3D%20self.head%0A%20%20%20%20%20%20while%20current%20!%3D%20None%3A%0A%20%20%20%20%20%20%20%20current.printNode%28%29%0A%20%20%20%20%20%20%20%20current%20%3D%20current.next%0A%0A%20%20%20%20def%20printSizeOfList%28self%29%3A%0A%20%20%20%20%20%20pass%0A%0Anode_a%20%3D%20Node%28%22A%22%29%0Anode_b%20%3D%20Node%28%22B%22%29%0Anode_c%20%3D%20Node%28%22C%22%29%0A%0Anode_a.next%20%3D%20node_b%0Anode_b.next%20%3D%20node_c%0A%0Alinked_list%20%3D%20LinkedList%28node_a%29%0Alinked_list.printList%28%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false)

One can use Python Tutor to visualize what happens in the memory addresses of the Python program during the creation of the `Node` and `LinkedList` class and the initialization of the objects `node_a`, `node_b`, `node_c`, and `linked_list`. If you are feeling curious, click the link above and walk through the program line by line to see what happens in the program's memory during execution.
