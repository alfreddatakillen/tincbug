# Testbed for some strange behaviour in Tinc

Just a couple of `Dockerfile`s for testing some strange potential bug in
Tinc 1.1pre14.

It seemed like Tinc would start bugging out after too many invites/joines,
but we can not repeat that error here.

## batman

So, first I start the batman machine:

	cd batman
	docker build -t batman .
	docker run --device=/dev/net/tun --cap-add NET_ADMIN batman

Now, I get invites (replacing `c5358ceebaa8` with whatever container id batman
is running with):

	docker exec c5358ceebaa8 "/usr/local/sbin/tinc -n superheroes invite robin"

## robin

	cd robin
	docker build -t robin .

Now, I create an invite and use it to join robin (over and over again), running
this command multiple times (again, replacing `c5358ceebaa8` with whatever
container id batman is running with):

	docker run --link=c5358ceebaa8:batman robin "/usr/local/sbin/tinc join $(docker exec c5358ceebaa8 "/usr/local/sbin/tinc -n superheroes invite robin$(date +%s)")"

## AND IT FREAKIN' WORKS OVER AND OVER AGAIN, SO SOMETHING ELSE IS WRONG HERE, NOT TINC!


