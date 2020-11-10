# HierarchicalStateMachineForUnity
A hierarchical state machine implementation for Unity


Every state in the machine is defined by a list of behaviours. 
The machine keeps a list of all the currently active behaviours.
The behaviours have an Update(), an Enter() an an Exit() method amongst other methods.
Enter() is called when the behaviour is added to the active behaviours list.
Update() is called every frame if the behaviour is currently in active behaviours list.
Exit() is called when the behaviour is removed from the active behaviours list.
When the machine transitions from state A to state B

  1. All of the behaviours present in state A that are not present in state B are removed, Exit() is called on them.
  2. All the behaviours present in state B that were not present in state A are added, Enter() is called on them.
  3. Then every frame Update() is called on every active behaviour

example:
State A = [o, p, q, x]    //state A consists of behaviours o,p,q,x
State B = [o,x,y,z]	      //state B consists of behaviours o,x,y,z

If we transition from A to B we will call the following methods in this exact order:
	q.Exit()
	p.Exit()
	y.Enter()
	z.Enter()
and then as long as the machine stays in state B, the behaviours o,x,y,z will get Update() called every frame.
