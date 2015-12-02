<h1 align="center">
  AI Game Competition 2, Sponsored by Google
</h1>

1. YOU MUST BE CONNECTED TO USC GUEST WIFI
  Send post requests to http://10.120.126.50:8080/
  The SERVERNAME will be anounced at the event.

  1. First create an account(new user) by sending a post request to /user/new with email, password, and username

    * curl --data "username=kappa&password=qw&email=yourEmail@yahoo.com" http://10.120.126.50:8080/user/new

  2. Afterwards, you configure your hero.

    * curl --data "username=kappa&password=qw&email=daea3@yahoo.com&radius=1&speed=1&number=0&move=0&vision=3" http://10.120.126.50:8080/user/config

    There are starting values for the attributes, and sum of all the additional attributes is 5.
    Radius: Radius of the bomb explosion. Default is 0.
      R = 1 means:  
      XXX
      XbX         //b stands for bomb
      XXX
    Speed: The max distance you can move bombs. Default is 3.
    Number: Number of initial bombs. Default is 2.
    Move: The max distance you can move each turn. Default is 2.
    Vision: The range you can see around you. Refer to radius for vision. Default is 1.


2. Join a game by sending a request to /game/join with parameters username and password.
  
  * curl --data "username=kappa&password=qw" http://10.120.126.50:8080/game/join
  
3. Move your hero by sending a request to /game/move with parameters username, password, move, direction, and distance.
  
  * curl --data "username=kappa&password=qw&move=S&direction=R&distance=2" http://10.120.126.50:8080/game/move

  move: S is "shoot" a bomb. M is move your hero.
  direction: U(up), D(down), L(left), R(right).
  distance: a non-negative integer.

4. Map is a 20*20 grid. (0,0) is top left and (19, 19) is bottom right. Each cell is a variable:
  "1": Player 1.
  "2": Player 2.
  "0": empty.
  "X": Obstacle.
  Objects:
  "N": Number of bombs ++. 
  "S": Speed(distance) of bomb ++.
  "M": Move ++.
  "V": Vision ++.
  "R": Radius ++.

  You can pick up the Objects by walking over them(no need to stop at it).

5. Bomb will explode if it touches "X", "1" or "2". It will dispear if it does not hit any of those by end of its path.
