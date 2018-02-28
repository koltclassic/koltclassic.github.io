---
layout: default
title:  "Game Dev - Post 3"
date:   2018-02-28 12:00:00
categories: gamedev
---

# Game Dev - Post 3

I've been continuing the [Brackeys tower defense tutorial](https://www.youtube.com/watch?v=beuoNuK2tbk&list=PLPV2KyIb3jR4u5jX8za5iU1cqnQPmbzG0) that I began in my last blog post. I believe that I had ended the last blog post at a point where I had the map created, the enemy paths defined and the wave spawner created, as well as a "basic tower" prefab that I will use as the standard tower to create. Since then, I have added in a turret's ability to find an enemy, shoot at that enemy, and damage / destroy an enemy. I've also implemented the placement of the standard tower onto the board and simple camera controls for the user.

One aspect of the tutorial explained how to make a turret rotate naturally toward an enemy to gradually "lock on", rather than an immediate centering. This natural rotation involved the use of Quaternions. I'm honestly not currently confident in my ability to accurately explain how or why Quaternions were used, but the Unity documentation will hopefully clear some things up for me (located [here](https://docs.unity3d.com/Manual/QuaternionAndEulerRotationsInUnity.html)).

I also learned about Gizmos for the first time.
The official Unity documentation definition:
> Gizmos are used to give visual debugging or setup aids in the scene view.

Gizmos were used to get a sense for the shooting radius that a turret had when created. The Gizmo was drawn using the `OnDrawGizmosSelected()` method, and the "drawing" used to represent the shooting radius was a wireframe sphere.

```C#
    void OnDrawGizmosSelected()
    {
        Gizmos.color = Color.red;
        Gizmos.DrawWireSphere (transform.position, range);
    }

```

With this method added, I could visually understand the difference between different turret ranges.
![]({{ "/assets/GizmoRange15.png" | absolute_url }})
*A turret with a wireframe sphere showing a range of 15*
![]({{ "/assets/GizmoRange5.png" | absolute_url }})
*A turret with a wireframe sphere showing a range of 5*

Understanding performance is a recurring theme of learning Unity. There always seem to be a more performant way to do things, which can become a constant worry when developing both in creating games and for programming in general. Performance was highlighted in the tower defense tutorial via the calculation that is done on towers to find nearby enemies to target. To prevent this calculation from happening much too often, an `InvokeRepeating` method was added to the `Start` function:

```C#
    void Start () {
        InvokeRepeating ("UpdateTarget", 0f, 0.5f);
    }
```

The third parameter of the `InvokeRepeating` method is the repeat rate (In this case, `0.5f`). The great thing about this repeat rate is that it "throttles" the amount of times that the function is called. There isn't currently any good reason that a tower would need to calculated the closest enemy 60 times a second, so having this calculation only be done twice a second is a quick and easy performance gain.

Some other quick notes:

- Header files are great: They seem to be very useful for organizing public variables in the Unity editor
- The differentiation between Local Space and World Space is something to always keep in mind and can influence things such as camera zoom.
  - Another note about camera zoom: Remembering that you have to restrict a user from zooming in past the game space, zooming out to a distance that makes the game space too tiny to see, etc. is just another funny aspect of programming to me.
- Object casting is also something to always keep in mind. For example, in the `Shoot()` method of the tower (which is used to shoot a bullet from a tower), you first have to instantiate a Bullet GameObject to "shoot" out of the turret. This instantiation looks like this:
  - `GameObject bulletGO = (GameObject) Instantiate (bulletPrefab, firePoint.position, firePoint.rotation);`

  Since Instantiating an Object does exactly that, you have to specify that the Object is a GameObject.
- Singleton usage for a "Game Manager". I'm still trying to fully understand this, but I think it makes sense to have a global source for things like which turrets are available to build. I would assume that things like general turret price would be stored here as well, while things like turret upgrades would be stored directly on the individual turret prefab instance.
