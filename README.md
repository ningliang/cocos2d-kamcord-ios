# Kamcord 0.9.4

## Code

The code is available at the following git repository: <a href="https://github.com/kamcord/cocos2d-kamcord-ios">https://github.com/kamcord/cocos2d-kamcord-ios</a>.

Please add yourself as a watcher since we frequently release new features and patches.

## Introduction

Kamcord is a built-in gameplay video and audio recording technology for iOS. This repository contains a Kamcord SDK that works with cocos2d-1.0.1 and allows you, the game developer, to capture gameplay videos with a very simple API.
Your users can then replay and share these gameplay videos via YouTube, Facebook, Twitter, and email.

In order to use Kamcord, you need a developer key and developer secret. To get these, please sign up at <a target="_blank" href="http://kamcord.com/signup">http://kamcord.com/signup</a>.

**Kamcord works on iOS 5+ and gracefully turns itself off on iOS 4**. You can still run without problems on versions of iOS before iOS 5, though you will not be able to to record video. Kamcord works on the iPhone 3GS, iPhone 4, iPhone 4S, iPod Touch 3G and 4G, and all iPads.

We will be making lots of improvements and adding many features over the next few months. We'd love to hear your feedback and thoughts. If you have any questions or comments, please don't hesitate to email or call Matt at <a href="mailto:matt@kamcord.com">matt@kamcord.com</a> (650.267.1051).

## Gameplay Recordings

Check out some gameplays recorded with Kamcord:

<p>
	<ul>
	<li>
		<a target="_blank" href="http://www.youtube.com/watch?v=C4yM_iZSKxk">Mr. Ball</a> (<a target="_blank" href="http://itunes.apple.com/us/app/mr.-ball/id521546799">Apple App Store</a>)
	</li>
	<li>
		<a target="_blank" href="http://www.youtube.com/watch?v=rpPb2NhlD0Q">Platform Hell</a> (<a target="_blank" href="http://itunes.apple.com/us/app/platform-hell-pro/id428765417">Apple App Store</a>)
	</li>
	<li>
		<a target="_blank" href="http://www.youtube.com/watch?v=R2zqZ0FJ6yI">Adhesion</a> (<a target="_blank" href="http://itunes.apple.com/us/app/adhesion/id501869784">Apple App Store</a>)
	</li>
	<li>
		<a target="_blank" href="http://kamcord.com/v/8Pm4x61dTEQ/">Sewar Wars</a> (<a target="_blank" href="http://www.sewerwars.com">Website</a>)
	</li>
	<li>
		<a target="_blank" href="http://kamcord.com/v/D2I3G5o8dO/">Carl The Spider</a> (<a target="_blank" href="http://itunes.apple.com/us/app/carl-the-spider/id504163507">Apple App Store</a>)
	</li>
	<li>
		<a target="_blank" href="http://kamcord.com/v/So5sOMb8pn/">Atlantis Oceans</a> (<a target="_blank" href="http://itunes.apple.com/us/app/atlantis-oceans/id384836591">Apple App Store</a>)
	</li>
	</ul>
</p>
	

## A Sample Application

Before we explain how to use Kamcord in your own applications, let's go through a quick example that runs right out the box. Clone this repository to your local machine and open the project located at `Examples/cocos2d-iphone-1.0.1/cocos2d-ios.xcodeproj`.  Select `RotateWorldTest` from the dropdown and build and run that application. You should see the familiar `RotateWorldTest` from the Cocos2D suite of tests. **Make sure to run the application on a physical device with iOS 5+, not the simulator. Video replay is NOT supported by the simulator!**

After 10 seconds, the Kamcord view should appear allowing you to replay a video recording of those first 10 seconds and share that video via Facebook, Twitter, YouTube, and/or email. `ParticleTest`, `SceneTest`, and `SpriteTest` all work the same way.

`RenderTextureTest` is different in that it allows you to start and stop recording by pressing the two corresponding buttons at the top right of the screen. When you press `Stop Recording`, you will again see the Kamcord view with options to replay and share. Later on in this documentation, we'll walk through all the code needed to add recording and replay functionalities to `RenderTextureTest`.

There is no practical limit on how long you can record for. Everything gets written immediately to disk and old videos are always being erased, so the only real limitation is the device's hard drive size. Since modern iOS devices have 16+ GB of hard disk space, you can safely record one continuous gameplay video for over 24 hours straight, an upper limit your gamers will probably never run into.

## Installation

Let's walk through how to get Kamcord into your games.

### Framework

<ol>
<li style="margin: 0";>From <code>Frameworks</code>, drag and drop <code>Kamcord.framework</code> and <code>AWSiOSSDK.framework</code> into your project.
<p>
<img src="https://dl.dropbox.com/u/6122/Kamcord/Kamcord%20Frameworks.png" />
</p>
</li>
<li style="margin: 0";>Drag and drop the files under <code>Frameworks/Resources</code> to your project. For both this and the previous step, make sure to check the box next to the target application you want to link these frameworks and resources to (your game, presumably).
<p>
<img src="https://dl.dropbox.com/u/6122/Kamcord/Resources.png" />
</p>
</li>
<li style="margin: 0";>Ensure you have the following frameworks under <code>Build Phases</code> ==> <code>Link Binary With Libraries</code>:
	<p>
		<ul style="margin-top: 15px; margin-bottom: 15px;">
			<li style="margin: 0;">Accounts</li>
	        <li style="margin: 0;">AVFoundation</li>
	        <li style="margin: 0;"><b>AWSiOSSDK</b></li>
	        <li style="margin: 0;">CoreData</li>
	        <li style="margin: 0;">CoreGraphics</li>
	        <li style="margin: 0;">CoreMedia</li>
	        <li style="margin: 0;">CoreVideo</li>
	        <li style="margin: 0;">Foundation</li>
	        <li style="margin: 0;"><b>Kamcord</b></li>
	        <li style="margin: 0;">MediaPlayer</li>
	        <li style="margin: 0;">MessageUI</li>
	        <li style="margin: 0;">OpenGLES</li>
	        <li style="margin: 0;">QuartzCore</li>
	        <li style="margin: 0;">Security</li>
	        <li style="margin: 0;">SystemConfiguration</li>
	        <li style="margin: 0;">Twitter</li>
	        <li style="margin: 0;">UIKit</li>
	    </ul>
    </p>
    <p>
    	<img src="http://dl.dropbox.com/u/6122/Kamcord/Frameworks.png" />
    </p>
    <p>
    <b>To support iOS 4 deployment, set the frameworks inside the orange box to <code>Optional</code>. This will allow your app to run on devices with iOS 4 and ensures Kamcord functionality will gracefully silence itself on iOS 4 as if you had never installed Kamcord.</b>
    </p>
</li>
<li style="margin: 0;">Add the following to <code>Build Settings</code> ==> <code>Other Linker Flags</code>:
	<p>
    <ul style="margin-bottom: 15px;">
        <li style="margin: 0;">-ObjC</li>
        <li style="margin: 0;">-all_load</li>
        <li style="margin: 0;">-lxml2</li>
    </ul>
    </p>
    <p>
    <img src="http://dl.dropbox.com/u/6122/Kamcord/other_linker_flags2.png"/>
    </p>
</li>
</ol>

### Code

<ol>
<li>
<p>
Import Kamcord into your application delegate:

<pre><code>#import &lt;Kamcord/Kamcord.h&gt;
</code></pre>
</p>
</li>
<li>We will provide you with a per-game Kamcord developer key and developer secret. Please set them along with your app name when your app initializes or recording won't work.
<p>
<pre><code>[Kamcord setDeveloperKey:@"My_Developer_Key"
         developerSecret:@"My_Developer_Secret"
                 appName:@"My_Game_Name"];</code></pre>
</p>
</li>
<li style="margin: 0;">
<p>
In your application delegate (or wherever you create the <code>UIWindow</code> and initialize <code>CCDirector</code>), instantiate a <code>KCGLView</code>. This is our special sublcass of <code>EAGLView</code> that aids in video recording. Then set <code>window.rootViewController</code> to an instance of <code>KCViewController</code> and set <code>window.rootViewController.view</code> to your <code>KCGLView</code>. If you have any other view controllers, comment them out.
</p>
<p>
<b>Also be sure to use </b><code>[Kamcord setDeviceOrientation:...]</code> <b>instead of</b> <code>[director setDeviceOrientation:...]</code>:
</p>

<p>
<pre><code>// Instantiate a KCGLView, which is a subclass with EAGLView with
// special recording functionality.
KCGLView * glView = [KCGLView viewWithFrame:[window bounds]
                                pixelFormat:kEAGLColorFormatRGB565
                                depthFormat:0];

// Kamcord uses UIKit for autorotation, which requires special logic to handle rotations.
window.rootViewController = [[KCViewController alloc] initWithNibName:nil bundle:nil];
window.rootViewController.view = glView;

// Tell Kamcord about the root view controller and the KCGLView
[Kamcord setParentViewController:window.rootViewController];
[Kamcord setOpenGLView:glView];

// Set the device orientation. <b>Must use Kamcord, not CCDirector!</b>
[Kamcord setDeviceOrientation:CCDeviceOrientationLandscapeLeft];
</code></pre>
</p>
<p>
This must all be done before:

<pre><code>[window addSubview:glView];
[window makeKeyAndVisible];
</code></pre>
</p>
<p>
The full examples further below lay this out very clearly.
</p>
</li>
</ol>

Your project should build successfully at this point.

## How to use Kamcord

We've tried to keep the Kamcord API as simple as possible. The only class you will need to interface with is `Kamcord`, which you can get by importing `<Kamcord/Kamcord.h>`.

Kamcord's public API is broken down by different functionalities.

### Video Recording

The recording interface is built around the concept of one video, which has one or more clips. Most videos will just have one clip, but if your game is interrupted (for example, if the user gets a phone call), you'll have several clips that need to be stitched together into one seamless video. Kamcord handles all of that behind the scenes as long as you pause and resume your recording at the appropriate places in the app lifecycle.

The API is:

    + (void) startRecording;
    + (void) stopRecording;
    + (void) pause;
    + (void) resume;

`startRecording` starts the video recording, which you can pause and resume with `pause` and `resume`. Once you're done with the entire video, call `stopRecording`.

**Please be aware that video replay will NOT work in the simulator! The video will be recorded and it will be the right length, but it will be all black. You must test on a device to see the video replay actually work.**

### Video Quality

You can set the resolution of the recorded video:

	+ (void) setVideoResolution:(KC_VIDEO_RESOLUTION)resolution;

There are two video resolution settings:

- `SMART_VIDEO_RESOLUTION`: 512x384 on iPad 1 and 2, 1024x768 on iPad , and 480x320 on all iPhone/iPods.
- `TRAILER_VIDEO_RESOLUTION`: 1024x768 on all iPads, 480x320 on non-retina iPhone/iPods, and 960x480 on retina iPhone/iPods.

`SMART_VIDEO_RESOLUTION` is the default setting and should be used when you deploy your game. As the name suggests, `TRAILER_VIDEO_RESOLUTION` is only intended for you to make trailers with. Releasing your game with `TRAILER_VIDEO_RESOLUTION` is **strongly** discouraged. It will eat up your user's data plan, CPU, game resources (FPS), battery and result in video uploads that are more than five times longer (and thus potentially more network failures).

We currently don't support recording at iPad retina resolutions (2048x1536) because it seems that Apple doesn't support writing videos of those resolutions, but we plan to come back to this issue in the future.

### Audio Recording

As of version 0.9.2, you can overlay your game's audio to the recorded video with the following API calls:

	+ (KCAudio *) playSound:(NSString *)filename
    	               loop:(BOOL)loop;
	+ (KCAudio *) playSound:(NSString *)filename;

The second function call simply calls the first with `loop` set to `NO`. These sounds *are not sent to the speakers*, but will be added to the recorded video at the exact time you call `playSound`. The intended use of these methods is to pair calls to `CocosDenshion` (or whichever sound engine you use) with calls to `Kamcord` like so:

	// One time sounds
	[[SimpleAudioEngine sharedEngine] playEffect:@"sound.wav"];
	[Kamcord playSound:@"sound.wav"];
	
	// Background sounds
	[[SimpleAudioEngine sharedEngine] playBackgroundMusic:@"background.mp3"];
	[Kamcord playSound:@"background.mp3" loop:YES];

If you'd ever like to stop a sound from playing in the recording, you can save the `KCAudio *` object that is returned by `playSound` and call `stop` on that object. You don't need to call `start` on the returned `KCAudio` object, `[Kamcord playSound:]` will take care of that for you.

For convenience, we've added a method to stop all sounds:

	+ (void) stopAllSounds:(BOOL)loop;
	
If `loop` is `NO`, this will only stop non-looping sounds. If `loop` is `YES`, this will stop ALL sounds.

The `RenderTextureTest` example below shows how to record sound.

**Note that this audio track is only overlayed on the video once the video processing is finished.** We begin video processing in the background as soon as you call stopRecording, but the video you watch via the Replay Video button on the Kamcord UI may show the preprocessed video (without the audio overlay). Don't worry, the final video that is shared on Facebook/Twitter and uploaded to YouTube *will* have the sounds overlayed.

We are currently working on adding the played sounds to the replayed video. In the future, we intend to wrap calls to `CocosDenshion` so that you don't have to worry about pairing sounds calls together.

### Presenting User Options

Now that the user has finished his gameplay and you have successfully recorded a video of it, you can present several options to the user with the following API call:

	+ (void) showView;

This presents the following modal view:

<img src="https://dl.dropbox.com/u/6122/Kamcord/MainMenu.png" style="display: block; margin-left: auto; margin-right: auto;" />

Pressing the play button will replay the last recorded video (the result of the last `stopRecording` call).

Pressing any of the four buttons below will let the user share on Facebook/Twitter/YouTube and with Email:

<img src="https://dl.dropbox.com/u/6122/Kamcord/ShareView.png" style="display: block; margin-left: auto; margin-right: auto;" />

The first time the user presses the share button on this view, he will be prompted for the relevant credentials and permissions.

This view is built programmatically, so there are no storyboards or nibs to mess with.

All uploading to YouTube and sharing on Facebook/Twitter happens in a background thread. This provides for a great user experience because your user can share/upload in the background and and get back to playing your game as soon as possible.

On Facebook, we will share the URL of the video with their typed message. A thumbnail from the video will be automatically generated and shown. On Twitter, if the user types the following message:

`Check out my gameplay!`

the actual tweeted message will be

`Check out my gameplay! kamcord.com/v/abcfoo123`

### Downloading Video Trailers

To get to the recorded videos from your device, click on `Window` ==> `Organizer`, select your device on the left hand side, and select your app from the apps list:

<img src="https://dl.dropbox.com/u/6122/Kamcord/Organizer.png" />

Click the `Download` button at the bottom of the window and you should get a folder on your computer that is a full copy of your device's filesystem. You can then browse to `Documents/Kamcord` and find the `GUID__coverted.mov` for your trailer.

### Differences from Cocos2D

If your application's setup code calls `CC_DIRECTOR_INIT()`, replace it with `CC_DIRECTOR_INIT_KAMCORD()` and add the following two lines after `[Kamcord setDeviceOrientation:...]` is called:

	[window addSubview:[[CCDirector sharedDirector] openGLView];
    [window makeKeyAndVisible];
    
`ParticleTest`, `RotateWorldTest`, `SceneTest`, and `SpriteTest` all show how to use `CC_DIRECTOR_INIT_KAMCORD()`. Their source code can be found in `Examples/cocos2d-iphone-1.0.1/tests`.

Kamcord uses <a href="http://www.cocos2d-iphone.org/wiki/doku.php/prog_guide:autorotation#the_uikit_autorotation"/>UIKit for autorotation</a>. <b>To ensure everything works as advertised, please make your </b>`window.rootViewController` <b>an instance of </b>`KCViewController` and use

	[Kamcord setDeviceOrientation:...]

instead of `[[CCDirector sharedDirector] setDeviceOrientation:...]`. If you cannot make your `window.rootViewController` an instance of `KCViewController`, <a href="mailto:matt@kamcord.com" />let us know</a> and we'll give you a simple patch for your View Controller code.

<b>If your code queries </b><code>[[CCDirector sharedDirector] deviceOrientation]</code><b>, replace all of those calls with </b><code>[Kamcord deviceOrientation]</code>.

If you set either `CCDeviceOrientationLandscapeLeft` or `CCDeviceOrientationLandscapeRight`, Kamcord will autorotate the screen to support both landscape orientations.

### Developer Settings

A YouTube video looks like this:

<img src="http://dl.dropbox.com/u/6122/Kamcord/youtube_video2.png"/>

You can set the title, description, and keywords (highlighted in the orange boxes) with the following function:

	+ (void) setYouTubeTitle:(NSString *)title
     	         description:(NSString *)description 
                    keywords:(NSString *)keywords;

`youtubeKeywords` is one string of word tokens delimited by commas (e.g. `"multi-word keyword, another multiword keyword, keyword3, keyword4"`).

A Facebook wall post looks like the following:

<img src="http://dl.dropbox.com/u/6122/Kamcord/facebook_share.png"/>

The `Message` is the text the user will enter. You can set the title, caption, and description with the following function:

	+ (void) setFacebookTitle:(NSString *)title
   	                  caption:(NSString *)caption
                  description:(NSString *)description;

When the user shares to Facebook, their video is first uploaded to Kamcord. We will then use your settings to populate the corresponding fields on Facebook. Needless to say, this is a great way to advertise your game by putting links to your website or your game's page on the Apple App Store.

It's worth noting that every time we post to Facebook, we use the currently set values of these fields. Therefore, you may want to change the title, caption, and or description to match the results of the most recent gameplay. We recommend you do this so that the message looks more customized which should result in more clicks on the video.

Another function you need to set after you call `stopRecording` is:

	+ (void) setLevel:(NSString *)level
     	        score:(NSNumber *)score;
	
These values should be set per video. This metadata will be uploaded along with the video and be used to better organize videos for viewers.

### Developer Key, Secret, and Application Name

You must set your Kamcord developer key, secret, and app name using this function:

	+ (void) setDeveloperKey:(NSString *)key
	         developerSecret:(NSString *)secret
	                 appName:(NSString *)name;

We will give you a key and secret per game you build. We'll give you as many key/secret pairs you need, just don't tell them to anyone else.


## Examples

The `Examples` directory has some fully functional examples of how to use Kamcord in your application. You will recognize these as test apps that come bundled with Cocos2D. The following test apps have been ported over to `Kamcord`:

<ul>
    <li style="margin: 0;">ParticleTest</li>
    <li style="margin: 0;">RenderTextureTest</li>
    <li style="margin: 0;">RotateWorldTest</li>
    <li style="margin: 0;">SceneTest</li>
    <li style="margin: 0;">SpriteTest</li>
</ul>

### RenderTextureTest

When this app launches, there are six buttons on the top right of the screen. The top two control video recording and the next four control which sounds are played. Play around by pressing `Start Recording`, doing some drawing or flipping between different tests, playing and stopping a couple of sounds, and then pressing `Stop Recording`. The Kamcord dialog should pop up and you'll be able to replay a video recording of your actions as well as share that video online. Note that the audio overlay will only be available after the video has finished processing. We are working on adding audio overlay to the pre-processed video also.

Below are all of the code integration points inside `Examples/cocos2d-iphone-1.0.1/tests/RenderTextureTest.m`. We bold the lines we added to make Kamcord work. First, include the library:

<pre><code><b>#import &lt;Kamcord/Kamcord.h&gt;</b>
</code></pre>

Then do all the Kamcord initialization:

<pre><code>- (void) applicationDidFinishLaunching:(UIApplication*)application
{
	// Init the window
	window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
	
	// must be called before any other call to the director
	[CCDirector setDirectorType:kCCDirectorTypeDisplayLink];
	
	// before creating any layer, set the landscape mode
	CCDirector *director = [CCDirector sharedDirector];
	
	// set FPS at 60
	[director setAnimationInterval:1.0/60];
	
	// Display FPS: yes
	[director setDisplayFPS:YES];
	
	<b>
	// Instantiate a KCGLView, which is a subclass with EAGLView with
	// special recording functionality.
	KCGLView * glView = [KCGLView viewWithFrame:[window bounds]
                                    pixelFormat:kEAGLColorFormatRGB565
                                    depthFormat:0];

	// Kamcord uses UIKit for autorotation, which requires special logic to handle rotations.
	window.rootViewController = [[KCViewController alloc] initWithNibName:nil bundle:nil];
	window.rootViewController.view = glView;

	// Tell Kamcord about the root view controller and the KCGLView
	[Kamcord setParentViewController:window.rootViewController];
	[Kamcord setOpenGLView:glView];

	// Set the device orientation. Must use Kamcord, not CCDirector!
	[Kamcord setDeviceOrientation:CCDeviceOrientationLandscapeLeft];    
	
    // Developer settings
    [Kamcord setDeveloperKey:@"MY_DEVELOPER_KEY"
             developerSecret:@"MY_DEVELOPER_SECRET"
                     appName:@"A Test App"];
    
    // Social media settings
    [Kamcord setYouTubeTitle:@"RenderTextureTest"
                 description:@"This is a Cocos2D test app that was recorded with Kamcord."
                    keywords:@"Cocos2D RenderTextureTest"];
    
    [Kamcord setFacebookTitle:@"RenderTextureTest"
                      caption:@"Kamcord recording"
                  description:@"This is a Cocos2D test app that was recorded with Kamcord."];
    
    // Set a background audio track we're going to loop over the recorded video.
    [Kamcord setAudioResourceName:@"background"
                        extension:@"wav"];
    </b>
	// 2D projection
    //	[director setProjection:kCCDirectorProjection2D];
	
	// Enables High Res mode (Retina Display) on iPhone 4 and maintains low res on all other devices
	if( ! [director enableRetinaDisplay:YES] )
		CCLOG(@"Retina Display Not supported");
	<b>
	// Not Kamcord specific, but don't forget to do this after
	// all the Kamcord initialization is finished.
	[window addSubview:glView];
	[window makeKeyAndVisible];
	</b>	
	// Default texture format for PNG/BMP/TIFF/JPEG/GIF images
	// It can be RGBA8888, RGBA4444, RGB5_A1, RGB565
	// You can change anytime.
	[CCTexture2D setDefaultAlphaPixelFormat:kCCTexture2DPixelFormat_RGBA8888];		
	CCScene *scene = [CCScene node];
	[scene addChild: [nextAction() node]];
	
	[director runWithScene: scene];
}
</code></pre>

This code sets up the window's root view controller and gives it ownership of the `KCGLView`. It then starts recording a new video. The `Start Recording` and `Stop Recording` buttons in the app are hooked in as follows:

<pre><code><b>@interface KamcordRecording ()

@property (nonatomic, retain) KCAudio * sound1;
@property (nonatomic, retain) KCAudio * sound2;

@property (nonatomic, retain) AVAudioPlayer * audioPlayer1;
@property (nonatomic, retain) AVAudioPlayer * audioPlayer2;

@end


@implementation KamcordRecording
{
    KCAudio * sound1_;
    KCAudio * sound2_;
    
    AVAudioPlayer * audioPlayer1_;
    AVAudioPlayer * audioPlayer2_;
}

@synthesize sound1 = sound1_;
@synthesize sound2 = sound2_;

@synthesize audioPlayer1 = audioPlayer1_;
@synthesize audioPlayer2 = audioPlayer2_;</b>

-(id) init
{
	if( (self = [super init]) ) {
		
		CGSize s = [[CCDirector sharedDirector] winSize];	
		
		// create a render texture, this is what we're going to draw into
		target = [[CCRenderTexture renderTextureWithWidth:s.width height:s.height] retain];
		[target setPosition:ccp(s.width/2, s.height/2)];
		
		
		// It's possible to modify the RenderTexture blending function by
		// [[target sprite] setBlendFunc:(ccBlendFunc) {GL_ONE, GL_ONE_MINUS_SRC_ALPHA}];
		
		// note that the render texture is a CCNode, and contains a sprite of its texture for convience,
		// so we can just parent it to the scene like any other CCNode
		[self addChild:target z:-1];
		
		// create a brush image to draw into the texture with
		brush = [[CCSprite spriteWithFile:@"fire.png"] retain];
		[brush setOpacity:20];
#ifdef __IPHONE_OS_VERSION_MAX_ALLOWED
		self.isTouchEnabled = YES;
#elif defined(__MAC_OS_X_VERSION_MAX_ALLOWED)
		self.isMouseEnabled = YES;
		lastLocation = CGPointMake( s.width/2, s.height/2);
#endif
		
		[CCMenuItemFont setFont"Size:16];
		<b>CCMenuItem *item1 = [CCMenuItemFont itemFromString:@"Start Recording" target:self selector:@selector(startRecording:)];
		CCMenuItem *item2 = [CCMenuItemFont itemFromString:@"Stop Recording" target:self selector:@selector(stopRecordingAndShowDialog:)];
		CCMenuItem *item3 = [CCMenuItemFont itemFromString:@"Play Sound #1" target:self selector:@selector(playSound1:)];
        CCMenuItem *item4 = [CCMenuItemFont itemFromString:@"Play Sound #2" target:self selector:@selector(playSound2:)];
        CCMenuItem *item5 = [CCMenuItemFont itemFromString:@"Stop Sound #1" target:self selector:@selector(stopSound1:)];
        CCMenuItem *item6 = [CCMenuItemFont itemFromString:@"Stop Sound #2" target:self selector:@selector(stopSound2:)];
		CCMenuItem *item7 = [CCMenuItemFont itemFromString:@"Stop All Sounds" target:self selector:@selector(stopAllSounds:)];
		CCMenu *menu = [CCMenu menuWithItems:item1, item2, item3, item4, item5, item6, item7, nil];</b>
		[self addChild:menu];
		[menu alignItemsVertically];
		[menu setPosition:ccp(s.width-80, s.height-<b>90</b>)];
	}
	return self;
}

<b>-(void) startRecording:(id)sender
{
    [Kamcord startRecording];
}

-(void) stopRecordingAndShowDialog:(id)sender
{
	[Kamcord stopRecording];
    [Kamcord showView];
}

-(void) playSound1:(id)sender
{
    if (!self.audioPlayer1)
    {
        NSURL * url = [[NSBundle mainBundle] URLForResource:@"test8" withExtension:@"caf"];
        self.audioPlayer1 = [[AVAudioPlayer alloc] initWithContentsOfURL:url error:nil];
    }
    
    if ([self.audioPlayer1 play]) {
        self.sound1 = [Kamcord playSound:@"test8.caf"];
    }
}

-(void) playSound2:(id)sender
{
    if (!self.audioPlayer2)
    {
        NSURL * url = [[NSBundle mainBundle] URLForResource:@"test3" withExtension:@"m4a"];
        self.audioPlayer2 = [[AVAudioPlayer alloc] initWithContentsOfURL:url error:nil];
    }
    
    if ([self.audioPlayer2 play]) {
        self.sound2 = [Kamcord playSound:@"test3.m4a"];
    }
}

-(void) stopSound1:(id)sender
{
    [self.audioPlayer1 stop];
    [self.sound1 stop];
}

-(void) stopSound2:(id)sender
{
    [self.audioPlayer2 stop];
    [self.sound2 stop];
}

-(void) stopAllSounds:(id)sender
{
    [self.audioPlayer1 stop];
    [self.audioPlayer2 stop];
    [Kamcord stopAllSounds:NO];
}
</b></code></pre>

For most games, you'll want to defer the calls to `startRecording` until appropriate (your user begins the actual level, etc.).

To highlight the handling of the application lifecycle, we've made additions to the following functions:

<pre><code>-(void) applicationWillResignActive:(UIApplication *)application
{
	[[CCDirecto shraredDirector] pause];
    <b>[Kamcord pause];</b>
}

-(void) applicationDidBecomeActive:(UIAplicpation *)applicaton
{i
    <b>[Kamcord resume];</b>
	[[CCDirector sharedDirector] resume];
}
</code></pre>

That's all you have to do to manage the applicaton lifecycle. If no video is currently being recorded (i.e. `startRecording` has not been called), the calls to `pause` and `resume` do nothing.

To test this functionality, press `Start Recording`, play with the app, then close it by pressing the home button. Re-open the app, do some more actions, then press `Stop Recording`. When the Kamcord dialog appears, select `Replay Video`. It should show one seamless video of everything that's happened.

<b>Note: in your game, you should defer calling</b> `resume` <b>until your user resumes gameplay. Calling it in</b> `applicationDidBecomeActive:` <b>like in this example will capture the pause screen of your game, which is probably not what you or your user wants.</b>

## Implementing Custom UIs

As of 0.9.4, we've added support that lets game developers create their own UIs that interact with Kamcord. Please add a small `Powered by Kamcord` to your sharing view along the same veins as with the stock UI.

You can replay the most recent video in a `UIViewController` of your choice:

    + (void)presentVideoPlayerInViewController:(UIViewController *)parentViewController;
    

You can also share the most recent video by plugging into our API. There are two options.

### Option 1: Kamcord handles Facebook/Twitter/YouTube auth

The Kamcord stock UI is built on top of this option. If you don't want to deal with the hassle of doing Facebook/Twitter/YouTube auth, you should use the following API calls:

    + (void)showFacebookLoginView;
    + (void)authenticateTwitter; 
    + (void)presentYouTubeLoginViewInViewController:(UIViewController *)parentViewController;

These functions pop up the Facebook login view, the Twitter auth alert view, and the YouTube login views, respectively. Once the user authenticates with these methods, Kamcord will store their credentials. You can verify the results of these authentication actions by implementing the following delegates inside the `KCShareDelegate` protocol:

    - (void)facebookAuthFinishedWithSuccess:(BOOL)success;
    - (void)twitterAuthFinishedWithSuccess:(BOOL)success;
    - (void)youTubeAuthFinishedWithSuccess:(BOOL)success;

If the authentication was successfuly, the value of `success` will be `YES`, else `NO`. You can also check the status of authentication and logout the user with these calls:

    + (BOOL)facebookIsAuthenticated;
    + (BOOL)twitterIsAuthenticated;
    + (BOOL)youTubeIsAuthenticated;

    + (void)performFacebookLogout;
    + (void)performYouTubeLogout;

Once the user is authenticated to the relevant social networks, you can perform a share with those stored credentials with this API call:

    + (BOOL)shareVideoOnFacebook:(BOOL)shareFacebook
                         Twitter:(BOOL)shareTwitter
                         YouTube:(BOOL)shareYouTube
                     withMessage:(NSString *)message;

Simply set the values to YES for the networks you want to share to and give us the message the user wanted to share and we'll take care of the rest. One important note: this method returns `YES` if the request was accepted. If this returns `NO`, it means you tried to submit requests too quickly. More specifically, once you get one of the two following callbacks via the `KCShareDelegate` protocol:

    - (void)shareStartedWithSuccess:(BOOL)success error:(KCShareStatus)error;
    - (void)generalError:(KCShareStatus)error;
    
it will be safe to submit new share requests.

You will get callbacks about the status of the share via these callbacks from the `KCShareDelegate` protocol:

    - (void)facebookShareStartedWithSuccess:(BOOL)success error:(KCShareStatus)error;
    - (void)twitterShareStartedWithSuccess:(BOOL)success error:(KCShareStatus)error;
    - (void)youTubeUploadStartedWithSuccess:(BOOL)success error:(KCShareStatus)error;
    - (void)emailSentWithSuccess:(BOOL)success error:(KCShareStatus)error;

    - (void)facebookShareFinishedWithSuccess:(BOOL)success error:(KCShareStatus)error;
    - (void)twitterShareFinishedWithSuccess:(BOOL)success error:(KCShareStatus)error;
    - (void)youTubeUploadFinishedWithSuccess:(BOOL)success error:(KCShareStatus)error;
    
The last three indicate that the requested message has been posted on the relevant social network.

You can also share with email using the following method:

    + (void)presentComposeEmailViewInViewController:(UIViewController *)parentViewController
                                           withBody:(NSString *)bodyText;

for which the corresponding finishd callback is:

	- (void)emailSentWithSuccess:(BOOL)success error:(KCShareStatus)error;

### Option 2: Kamcord only uploads the video and returns a shareable video URL and you handle the Facebook/Twitter/YouTube authentication and sharing

The API for case 2 is much simpler because you are responsible for all the sharing. Kamcord will only upload the video to Kamcord (and Youtube if requested), after which we will call back via the `KCShareDelegate` protocol to let you know the online URL of the video and thumbnail.

To ask Kamcord to upload the videos, call:

    + (BOOL)shareVideoWithMessage:(NSString *)message
                  withYouTubeAuth:(GTMOAuth2Authentication *)youTubeAuth
                             data:(NSDictionary *)data;

All videos will get uploaded to Kamcord. If you want to upload to YouTube also, pass in a valid auth object for the `youTubeAuth` argument. Otherwise, leave that argument `nil`. You can also pass in a dictionary of data that we will return to you once the video is ready to share. As with Option 1, this method returns a BOOL telling you whether or not the request was accepted. If the returned value was `NO`, you need to try again at a later time (typically on the order of seconds).

The callback you will receive is either `generalError:` or the following:

    - (void)videoIsReadyToShare:(NSURL *)onlineVideoURL
                      thumbnail:(NSURL *)onlineThumbnailURL
                        message:(NSString *)message
                           data:(NSDictionary *)data
                          error:(NSError *)error;

You can use the video and thumbnail URLs to share to whichever social networks you like.


## Other Kamcord details

### Mixpanel

We collect analytics on user behavior. Specifically, we keep track of how often users replay videos, how often they share to social networks, which social networks they share to, etc. The information we track is purely aggregate statistics and **not** personally identifiable, so you can rest assured there are no privacy concerns for your end users.

### Amazon Simple Storage Service (S3)

Kamcord stores videos on Amazon S3, hence why we need `AWSiOSSDK.framework`.

## Troubleshooting

Below are various integration issues that some game developers have run into.

### Application crashes when you press [Done] on the main Kamcord view

Make sure that there is only **one** view controller in your application delegate, and barring some strange cases, that root view controller should be an instance of `KCViewController`. We've seen cases where people have had both a `RootViewController` and a `KCViewController` instantiated inside their app delegate. Removing the `RootViewController` solved the crash problems.

### Video uploads to kamcord.com don't succeed

Kamcord uploads videos in the background. This allows your user to get back to playing your game right away. Even after your app loses foreground, we still have 10 mins of time to upload. In the case that we can't finish it in those 10 minutes, we queue the job for next time the app regains foreground, and keep doing this until the video upload succeeds.

If you are testing Kamcord with XCode and press the `Stop` button too soon after you press `Share`, the video will most likely not have finished uploading. This is especially true for videos recorded with `TRAILER_VIDEO_RESOLUTION` since they are about 5x larger than those recorded with `SMART_VIDEO_RESOLUTION`. Videos also upload much more quickly on WiFi than 3G. To ensure the video upload succeeds, just leave the app running for a sufficient time and check the video on kamcord.com. 

### Link error: Duplicate symbols in SBJsonWriter.o and SBJsonParser.o

This is a collision that results from `AWSiOSSDK.framework`. This framework is necessary in order for us to upload videos to our servers. Unfortunately, Amazon was careless and didn't rename the popular JSON library `SBJson` when they built their framework.

To remove these collisions, for every file `SBJson*.o` that complains of duplicate symbols, simply remove the corresopnding `SBJson*.m` file.

### armv6

Kamcord only supports i386 and armv7. If you need an armv6 build for some reason, <a href="mailto:matt@kamcord.com" />shoot us an email</a>.

## Contact Us

If you have any questions or comments, don't hesitate to email or call Matt at <a href="mailto:matt@kamcord.com">matt@kamcord.com</a> (650.267.1051). We reply to every email!

