Super Duper Golf Game
====================
by Crazy Catty Computer
![cat flying-b](https://user-images.githubusercontent.com/87847364/230899237-d93fc0b0-77c2-46b5-8b70-8eb4618b78b7.svg)

_______________________________________________

![golf1](https://user-images.githubusercontent.com/87847364/230897115-9325ce6a-91da-4cff-8b9d-7fbd9ab434b0.JPG)


Introduction
------------
This game is a game which is made in [Unity](https://unity.com/).

It's a 3D golf game with high quality!

I made this project because I have a great interest in golf.


[CLICK HERE TO PLAY](Tim_Super_Duper_golf_WebGL_v3/index.html)


Instructions
-----------

  - Press `a` and `d` to rotate
  - Press space button to add force and make a strong hit
  - Try to reach the goal in a particular number of hits
  - Don't fall down!

Goal
----

You need to touch the flag which is in the end of the path to go to the next level (or to win).

How it works
-----------

The scripts are written in C#.

Here's some example snippets of code.

The code to hit the ball is bellow.

These lines are setting up variables.

  - `force` is for the hitting power
  - `is_increase` is for checking which way the force is changing
  - `ballRb` is a component "Rigidbody" on the object ball
  - `counts` is an interger which shows how many hits you have made
  - `limit` is another interger which can let the computer checked if you made so many hits
  - `goal_scene` is for reloading
~~~c
    float force = 5;
    bool is_increase = true;
    public Rigidbody ballRb;
    public int counts;
    public TextMeshPro tmp;
    public int limit;
    public string goal_Scene;
~~~

These lines bellow is for changing force.

First,it check the condition,is or not increasing.Then the program add or minus force by deltatime (time between each updates).

Then,to make it fancy,it change the length of the club.

At last,if the force is too big or small,switch the is_increasing variable to the other side.

~~~c
    void Update()
    {
        if (is_increase == true)
        {
            force += Time.deltaTime;
        }
        else
        {
            force -= Time.deltaTime;
        }
        transform.localScale = new Vector3(1, 1, force * 0.5f);
        if (is_increase && force >= 5)
        {
            is_increase = false;
        }
        if (is_increase!=true && force <= 0)
        {
            is_increase = true;
        }
~~~

These ones are the lines which make hits when the space button is pressed.

And it also will check if the counts(hits) is greater then limit.

If is,then reload the level.

~~~c
        if (Input.GetKeyDown("space"))
        {
            ballRb.AddForce(transform.forward *force, ForceMode.Impulse);
            counts += 1;
            tmp.text = counts.ToString();
            if (counts > limit)
            {      
                SceneManager.LoadScene(goal_Scene);
            }
        }
    }
~~~

The code for showing instructions works as follows:

~~~c
    float timer = 0;
    void Update()
    {
        timer += Time.deltaTime;
        if (timer >= 10)
        {
            Store.Instance.already_shown_instruction = true;
        }
        if (!Store.Instance.already_shown_instruction)
        {
            transform.Translate(-1.5f, 0, 0);
        } else
        {
            GetComponent<TextMeshProUGUI>().text = " ";
        }      
    }
~~~

Images
-------------

![golf2](https://user-images.githubusercontent.com/87847364/230894410-a59a077a-dfbb-418b-a970-3457fdad4adc.JPG)

Resources and Assets
--------------------
-[Kenny Assets](https://www.kenney.nl/assets)
