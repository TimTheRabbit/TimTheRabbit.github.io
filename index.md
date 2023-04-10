Super Duper Golf Game
=====================
by Crazy Catty Computer

Introduction
------------
This game is a game which is made in [Unity](https://unity.com/).

It's a 3D golf game with high quality~

I make this project because I have great interested in golf.

Instruction
-----------
-Press a and d to turn direction

-Press space button to add force and make a strong hit

-Try to reach in a particular number of hits

-Don't fall down!

Goal
-----
You need to touch the flag which is in the end of the path to go to the next level(or to win).

How it work
-----------
The script is written in C#.

Here's some good example:

The code for showing instruction-

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

The code to hit the ball-
~~~c
    float force = 5;
    bool is_increase = true;
    public Rigidbody ballRb;
    public int counts;
    public TextMeshPro tmp;
    public int limit;
    public string goal_Scene;

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

Sample images 
-------------
![golf1](https://user-images.githubusercontent.com/87847364/230894388-ab33035a-ce87-4dbe-87c4-9cf20d4f5563.JPG)

![golf2](https://user-images.githubusercontent.com/87847364/230894410-a59a077a-dfbb-418b-a970-3457fdad4adc.JPG)


Resources and Assets
--------------------
-[Kenny Assets](https://www.kenney.nl/assets)
