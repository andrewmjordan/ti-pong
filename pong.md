```perl
# Input sentinel?
1→Z
# Game tick
0→W
# Tick length
2→V
# P1 position
3→G
# P2 position
3→H
# Ball position
8→X
3→Y
# Ball velocity
(randInt(0,1)*2)-1→S
(randInt(0,1)*2)-1→T
# P1 score
0→A
# P2 score
0→B

# Choose speed
ClrHome
Menu("SPEED","SLOW",H,"MEDIUM",M,"FAST",R,"VERY FAST",W)
Lbl H
3→V
Goto 1
Lbl M
2→V
Goto 1
Lbl R
1→V
Goto 1
Lbl W
0→V

# Render initial frame
Output(Y,X,"o")
Output(G,1,"]")
Output(H,16,"[")

# Begin loop
# Input update
Lbl 1
Repeat Z<0
	getKey→θ
	If θ != 0
		Then
		-10→Z
	End
End

# Move P1 up
If θ=21 and G>1:Then:G-1→G:End
# Move P1 down
If θ=31 and G<7:Then:G+1→G:End
# Move P2 up
If θ=25 and H>1:Then:H-1→H:End
# Move P2 down
If θ=34 and H<7:Then:H+1→H:End

# Render current frame (again?)
ClrHome
Output(8,1,A)
Output(8,16,B)
Output(G,1,"]")
Output(H,16,"[")
Output(Y,X,"o")

# Physics update
W+1→W
If W>=V
Then
	X+S→X
	Y+T→Y
	0→W:
	# Vertical bounce
	If Y=1 or Y=7
	Then
		-1*T→T
	End
End

# Paddle collisions
If X=2 and Y=G or X=1 and Y=G
Then
	1→S
End
If x=15 and Y=H or X=16 and Y=H
Then
	-1→S
End

# P2 scored on P1
If X=0
Then
	1+A→A
	(randInt(0,1)*2)-1→S
	(randInt(0,1)*2)-1→T
	U→V
	8→X
	3→Y
End

# P1 scored on P2
If X=17
Then
	1+B→B
	(randInt(0,1)*2)-1→S
	(randInt(0,1)*2)-1→T
	U→V
	8→X
	3→Y
End

# Loop forever
Goto 1
```
