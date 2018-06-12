---

# Planets Yo!

---

Today we are going to show you how to make your very own little planet showcase Virtual reality experience.  

The Internet is so awesome that we dont need expensive software to create VR experiences we can do this simply by having an Internet connection, web browser and KNOWLEDGE.  

This is what you are going to be making.

![Planets Yo](https://www.dropbox.com/s/7sdfm9o3s5ugnn8/Screenshot%202018-06-12%2017.50.26.png?raw=1)


---

If you follow these steps you will be able to make it.  If you wish to do this in pairs this is fine.  We will be using something called Aframe.  Its a coding language you can using to make VR experiences in your web browser. You can learn more about [Aframe Here](https://aframe.io/).

Lets get cracking.

---

## Step One - Setup Environment
 
---

1. Please go to Glitch on a web browser.  [Click Here](https://goo.gl/nJh99a)

	![Glitch environment](https://www.dropbox.com/s/6o0324j1407dr50/Screenshot%202018-06-12%2020.22.44.png?raw=1)

2. In the main environment window top-left you will see planets-template. Click the drop down list and change the title to the name of your group - it can be whatever you want.

	![Change the name of the project to your own](https://www.dropbox.com/s/h059ytxq566o05o/Screenshot%202018-06-12%2020.24.17.png?raw=1)


3. In your main environment window you will see lines with code written on them.  In line four you will see: `<title>Hello</title>`

	Replace the hello with `<title>Planets VR YO!</title>`

	You have now changed the title of your page.


4. On the left menu you will see a list. One is called 'assets' click on that.  In here you will find some images.  We will be using these later. Go back to index.html.


---

## Step Two - Adding Assets

---

Now we have setup the environment we are going to do some coding to make our planets.  So that the planets look awesome we are going to add some images to them so they look realistic.

1. In your environment window line 17 is empty.  Type this: 


`<assets></assets>`


Games and rich 3D experiences traditionally preload their assets, such as models or textures, before rendering their scenes. This makes sure that assets aren’t missing visually, and this is beneficial for performance to ensure scenes don’t try to fetch assets while rendering.

We place assets within `<a-assets>`, and we place `<a-assets>` within `<a-scene>`. 

We can define our assets in <a-assets> and point to those assets from our entities using selectors.

Inside the assets tags type these three lines (Take care to do it right!). 

			<img id="earthTexture" src="" crossorigin="anonymous" />
			<img id="moonTexture" src="" crossorigin="anonymous" />
			<img id="starsTexture" src="" crossorigin="anonymous" />



2. Now we want to add some images so these look good.  To do this go to the assets folder.

3. You will see an image that looks like a world map. Click on it.

	![World map image](https://www.dropbox.com/s/mfhfgz4sv46s656/Screenshot%202018-06-12%2020.25.44.png?raw=1)

4. A button that says Copy URL will be there - Click it - this copies the URL you need.

	![Copy URL Button](https://www.dropbox.com/s/m399tnwib2wao5x/Screenshot%202018-06-12%2020.27.19.png?raw=1)

5. Go back to index.html and paste this in between the two speech marks in the `src=""` on earthTexture. From this:

		<img id="earthTexture" src="" crossorigin="anonymous" />

	to this


			<img id="earthTexture" src="https://cdn.glitch.com/ed2b5af6-	ce3b-425b-ac5f-a627fec24117%2Fearth.jpg?1528474412206" 		crossorigin="anonymous" />


6. Do the same for moon and stars
7. So you should have something that looks like this:


		<assets>
        	<img id="earthTexture" src="https://cdn.glitch.com/ed2b5af6-ce3b-425b-ac5f-a627fec24117%2Fearth.jpg?1528474412206" crossorigin="anonymous" />
        	<img id="moonTexture" src="https://cdn.glitch.com/ed2b5af6-ce3b-425b-ac5f-a627fec24117%2Fmoon.jpg?1528474410915" crossorigin="anonymous" />
        	<img id="starsTexture" src="https://cdn.glitch.com/ed2b5af6-ce3b-425b-ac5f-a627fec24117%2Fstars.jpg?1528476715908" crossorigin="anonymous" />
    	</assets> 


---

## Step Three - Add Stars

---

Getting to the good stuff now.  We have added the images we need to create the planets.

1. Before we begin I want you to look at the app viewer.  On the top right hand corner is a 'Show Live Button' Click this.  

	![Show Live Button](https://www.dropbox.com/s/4vlqphercrhj0c6/Screenshot%202018-06-12%2020.29.17.png?raw=1)
	
	A new window will open but the page at the minute still looks blank.  We will change that.

2. A scene is represented by the <a-scene> element. The scene is the global root object, and all entities are contained within the scene - basically its how we make a VR environment in a web browser.

3. Find line 17 and type this:

		`<a-scene>
			</a-scene> `

4. Inside the `<a-scene>`  type this: `<a-sky src="#starsTexture"></a-sky>`

	The `<a-sky>` is a primitive.  The sky primitive adds a background color 	or 360° image to a scene. A sky is a large sphere with a color or texture	 	mapped to the inside.

5. Now press the 'Show Live' button you should see Stars!

---

## Step Four - Add Planets

---

1. We have sky but we need some planets!

	Type this after `<a-sky>` but still within the `<a-scene>`.

	What we are doing is telling Aframe to make a sphere on the screen, the 	radius is the size, the position is the position on the screen. The src id 	#earthTexture is telling Aframe which image to use from the assets - which 	we did earlier.

		<a-sphere radius=".43441" position="1.2 1.5 -2" src="#earthTexture"></a-sphere>

	After this have a look at progress with the 'Show Live' button.  You should have an earth.

	But there is not much movement - we need rotation.  

2. Inside the `<a-sphere>` tags type this

		<a-animation attribute="rotation" dur="3000" easing="linear" to="0 360 0" repeat="indefinite"></a-animation>

So altogether it should look like this:

				<a-sphere radius=".43441" position="1.2 1.5 -2" 					src="#earthTexture">
    				<a-animation attribute="rotation" dur="3000" easing="linear" to="0 360 0" repeat="indefinite"></a-animation>
    		</a-sphere>
    
After this have a look at progress with the 'Show Live' button.  You should have a rotating earth.

---

## Step 5 - Make the Moon

---

Much like before we will create a sphere for the moon.  Just like the earth.

1. We tell Aframe to make another planet, position it, rotate and make it look a particular way. Type this:

   		<a-entity position="0 1.5 -2" rotation="10 90 0">
      		<a-sphere color="#FFF" radius=".23441" position="1 1.6 2.5" 							src="#moonTexture">
        	<a-animation attribute="rotation" dur="2000" 					easing="linear" to="0 360 0" repeat="indefinite"></a-animation>
      		</a-sphere>
    </a-entity>
      
	All we have done here is told Aframe to make another planet, position it, 	rotate and make it look a particular way.


2. Add text

	To finish off add this below.  This tag just adds a title in your VR window.

			<a-text value="Planets Yo!" width="6" position="-2.5 0.25 -1.5"

	Replace 'Planets Yo' with your Names.  

---

## How to View

To view this you can use the 'Show Live' button.  Its even more awesomer if you view this on your phone with a Google Cardboard.  Go to a browser on your phone (Chrome or Safari) and type in the URL of your project - (this is at the top of your window and it begins with `https:// ` )

Then place your phone in a Google Cardboard and enjoy!

---






