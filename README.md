This external community based and written guide is designed to answer the most madVR related questions by explaining each toggle. It's not official from the original author Mathias Rauen alias [madhsi](http://madvr.net/).

[![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/fold_left.svg?style=social&label=Follow%20%40CHEF-KOCH)](https://twitter.com/FZeven)
[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/CHEF-KOCH)
[![Discord](https://discordapp.com/api/guilds/204394292519632897/widget.png)](https://discord.me/NVinside)

Current MadVR version: [0.92.10](http://madshi.net/madVR.zip) - [Changelog](http://madshi.net/madVR/version.txt)


Guide Version: 0.0.1



Devices
--------

Device name: [EDID Product Name] A name for the display (customizable).<br/>

Device type: [unknown] Sets the icon for the display. When set to projector the 'screen config' section is available.<br/>

Identification:<br/>
EDID information, some displays are detected with different identifications depending on how they are attached or detected. You can drag and drop these identification entries to combine displays.<br/>


Properties:<br/>
The display expects the following RGB output levels: [PC levels (0-255)]<br/>
This is what your display expects to receive. 'PC levels (0-255)' means “use a 16-235 YCbCr to 0-255 RGB conversion matrix” and 'TV levels (16-235)' means “use a 0-255 YCbCr to 0-255 RGB conversion matrix”. If the source is flagged full range either a 0-255 YCbCr to 0-255 RGB or a 0-255 YCbCr to 16-235 RGB conversion matrix is used instead.<br/>

The native display bit-depth is: [8 bit] This is the bit depth madVR will dither to. madVR offers very high quality dithering so if you are using a low bit depth display (e.g. a 6-bit TN) you may get better quality setting this to 6-bit. It can be interesting to turn this down to a very low value (2-4) and test the various dithering options but make sure to have the 'trade quality for performance' option 'don’t use linear light for dithering' unchecked even if you leave it checked for normal use. Because of Windows, madVR dithers to 8-bit when set to 9 or 10-bit unless it is in D3D11 Full Screen Exclusive mode.<br/>


3D format: [auto] Set the 3D format for the display or swap left and right eyes.<br/>

Display peak luminance: [400 nits] Set the display's peak white brightness. This adjusts the amount of highlight compression to apply when displaying HDR content. A lower setting increases the brightness of mid range values.<br/>

calibration: [disable calibration controls for this display]<br/>
Disable calibration controls for this display: Disables all color gamut and gamma conversion functions.<br/>

This display is already calibrated: [BT.709, pure power curve, 2.20] This sets the current display characteristics. This affects the conversions used by madVR when playing video with a different gamut or using the 'enable gamma processing' option in 'color & gamma'.<br/>

calibrate this display by using yCMS: yCMS offers a simple gamut and gamma calibration method. It requires a few measurements of the display that can be done with [HCFR](http://sourceforge.net/projects/hcfr/). If gamut or grayscale measurements are not supplied only the other correction is performed. Usually bad results (mostly banding and odd effects in shadows) are obtained if gamma measurements below ~20% IRE are used so only enter values above 15-30% IRE.<br/>


calibrate this display by using external 3DLUT files: Use a calibration package such as Argyllcms, Calman, or LightSpace to generate a 256x256x256 3DLUT to perform a full calibration. For Argyllcms see this [AVS Forum thread](http://tinyurl.com/nx87y7c), for [Calman](http://tinyurl.com/map94jl), or for [LightSpace](http://www.lightillusion.com/madvr_manual.html).<br/>

Disable GPU gamma ramps: This disables the Windows calibration or monitor profile. It effects everything displayed, not only madVR. madVR will restore the profile when it is closed. This option changes its behavior when using the 'rendering -> general settings' option 'enable windowed overlay' to only apply to madVR because madVR is emulating the gamma ramps in that case.<br/>

display modes: [None]<br/>
Allows setting refresh rate and resolution automatically depending on the source video.<br/>

color & gamma: [Disabled]<br/>
pure power curve: [Default] use the standard pure power gamma function<br/>
BT.709/601 curve: use the inverse of a meant for camera gamma function. This has a linear section near black so shadows lighten faster as you move away from black. It can be helpful if your display has crushed shadows.
2.20, 2.40, etc.: [2.20] changes the display's gamma, based on the display's settings in 'calibration', to this target gamma. Without setting a calibration this option does nothing. Lower brightens mid range values which can be nice in a brightly lit room. Higher darkens mid range values which might look better in a darker room.

screen config: [Disabled]<br/>
This section is hidden unless the device is set as a projector.
define visible screen area by cropping masked borders: Allows scaling to a smaller resolution and adding black pixels to the edges. Useful if the projector is overshooting the edges of the screen. Only active when full screen.
activate lens memory number: Sends a command to a JVC or Sony projector to activate an on-projector lens memory number.
anamorphic lens: Allows output to non-square pixels.



Processing
----------


Deinterlacing:<br/>
if in doubt, activate deinterlacing: [Disabled] deinterlace video not flagged as progressive
if in doubt, deactivate deinterlacing: [Enabled] deinterlace video flagged as interlaced
force film mode: [Disabled] force IVTC, reconstructing the original progressive frames from video encoded as interlaced, decimating duplicate frames if necessary. IVTC (either auto or forced) is not functional if using native DXVA decoding because madVR's IVTC algorithm runs on the CPU instead of the GPU.<br/>
force video mode: [Disabled] force DXVA deinterlacing, uses the GPU's deinterlacing as set in its drivers.
only look at pixels in the frame center: [Enabled]<br/>


artifact removal: [Disabled]<br/>
reduce banding artifacts: Fade detection does not run if both options are set to the same value for a small increase in performance. Allowing all frames detected as part of a fade to be re-rendered using the higher setting removes five frames from madVR's rendering buffer every time a fade is detected.


image enhancements: [Disabled]<br/>
These are applied before scaling. See 'upscaling refinement'.<br/>


zoom control:<br/>
disable scaling if image size changes by only: [... 2 lines or less] If the resolution needs scaling by the number of pixels set or less no image scaling is done, black pixels are added to the right and/or bottom edge instead.<br/>

move subtitles: [... to bottom of the screen/window] Move subtitles, this is important when removing black bars or subtitles can be displayed outside the visible screen area.
automatically detect hard coded black bars: This enables the options below. This feature is designed to detect the black bars added to fit video content to other aspect ratios or the small black bars left from imprecise analog captures. For example, 16:9 video with black bars on the top and bottom encoded as 4:3 video or the few blank pixels on the left and right on a VHS capture. It can detect black bars on all sides.
if black bars change pick one zoom factor: Using this setting madVR will avoid changing the zoom or crop. e.g. It will not zoom or crop a 16:9 section in a normally 4:3 film when set to "which doesn't lose any image content" and will zoom or crop all of the 4:3 footage the amount needed to remove the black bars from any 16:9 sections when set to "which doesn't show any black bars".
if black bars change quickly back and forth: If not using the above option this option allows a limit on how often madVR can change the zoom or crop while playing to remove black bars as they are detected. Without either of these options madVR will always change the crop or zoom to remove all black bars.
notify media player about cropped black bars: How often to notify the media player of changes in the black bars.<br/>

always shift the image: This allows setting whether the top or bottom of the video is cropped when zooming.
keep bars visible if they contain subtitles: Disables zooming or cropping any black bar in which subtitles are detected. Either forever or for a set time.
cleanup image borders by cropping: Crop extra non-black pixels away from black bars or all edges. When set to crop all edges they are cropped even when no black bars are detected.
if there are big black bars: Allows setting separate handling of large black bars.
zoom small black bars away: This zooms into the video to remove the black bars, this usually results in cropping a small amount of video information off of one edge to maintain the original aspect ratio and resizing to the original display resolution. e.g. The bottom is cropped when cropping small black bars on the left and right and the video scaled to the original resolution.
crop black bars: This crops black bars, changing the display aspect ratio and resolution. Cropping black bars increases performance as the pixels no longer need to be processed. Profile rules referencing resolution will use the after crop resolution.<br/>


scaling algorithms
------------------

chroma upscaling: [Bicubic 75]<br/>
How madVR doubles the chroma resolution in both dimensions (assuming a YCbCr 4:2:0 source) to get YCbCr 4:4:4 before the conversion to RGB. When downscaling by a large amount this setting is used to bring the chroma to the target resolution instead of the luma resolution. Because madVR cannot use Jinc for downscaling Jinc falls back to Lanczos3 when downscaling the chroma.

image downscaling: [Catmull-Rom]<br/>
How madVR scales to the target resolution if it is smaller than the source.<br/>

image doubling: [Disabled]<br/>
Defaults: luma doubling = NNEDI3 32, chroma doubling = NNEDI3 16, quadrupling = NNEDI3 16
Uses super-xbr, NEDI, or NNEDI3 to perform 2x upscaling. If needed 'image downscaling' or 'image upscaling' is used to scale to the target resolution after doubling. If it is not doubled the chroma is upscaled to the target resolution using the options set in 'image upscaling'.<br/>

image upscaling: [Lanczos 3]<br/>
How madVR scales to the target resolution if it is larger than the source.<br/>

Nearest Neighbor: A very fast very low quality method, the closest pixel value is used, this looks very bad if not doing integer scaling (1x, 2x, 3x, etc.).<br/>
Bilinear: A very fast low quality method. This is as fast as Nearest Neighbor as GPUs can do bilinear filtering in a single operation.<br/>
DXVA2: Uses the GPU drivers or fixed function hardware to perform scaling. It is done in 8-bit so it may introduce banding or cause scaled dither noise. It can be very fast and low power. The quality varies between GPU brands and models. Image doubling cannot be used at the same time as DXVA2 scaling. Does chroma upscaling as well so this option overrides 'chroma upscaling'. Requires a restart of madVR to take effect. Does not bypass the graphics card's video (damage) algorithms so make sure they are off.
Mitchell-Netravali: Bicubic with b = 1/3, c = 1/3
Catmull-Rom: Bicubic with b = 0, c = 0.5
Bicubic: [50] Bicubic with b = 0, c = sharpness / 100, over 100 is a special case and should only be used for downscaling.
SoftCubic: [50] Bicubic with b = softness / 100, c = 0
Lanczos: [3] A sharp sinc type
Spline: [3] A different sinc type
Jinc: A more advanced sinc type (based on an EWA LanczosSharp from ImageMagick)
Bilateral: A chroma scaler that uses the luma channel as reference. This can be very good but it can fail too.<br/>
Reconstruction: [soft] Similar to Bilateral in that it uses luma channel information to aid chroma scaling. Soft is less prone to artifacts.
SSIM: Downscaling only. It is very sharp and detailed, especially useful with high downscaling ratios and fine details. with [Shiandow](http://tinyurl.com/hat4kbq)
super-xbr: [100] xBR means scale By Rules, it works by detecting edges and interpolating pixels along them. Can only perform a 2x upscale.
NEDI: New Edge-Directed Interpolation originally proposed by Xin Li and Michael Orchard. Can only perform a 2x upscale.<br/>
NNEDI3: [16] NNEDI3 (Neural Net Edge Directed Interpolation 3, original by tritical) implemented in OpenCL. Can only perform a 2x upscale but it can double X and Y independently. Below 32 neurons is not recommended for luma because 16 neurons are more likely to generate artifacts by connecting incorrect edges between smaller details. 16 neurons might be fine for chroma as chroma generally lacks small details. It uses the OCL D3D11 interop so it does not work in Windows XP.<br/>

activate anti-ringing filter: A post process method to reduce ringing, the major artifact caused by sharp bicubic and sinc type scalers.
scale in linear light: Using linear light when downscaling produces a result more similar to what one would get with optical scaling; bright specks such as stars in a night sky are preserved much better. The chroma is always upscaled to match the luma before downscaling when using this option because linear light downscaling is only possible in RGB. Not recommended for upscaling.
scale in sigmoidal light: Applies a sigmoidal curve after the power-like curve (or before when converting from linear to gamma-corrected). This helps reducing the dark halo artefacts around sharp edges caused by resizing in linear luminance.<br/>

upscaling refinement: [Disabled]<br/>
These are applied as part of upscaling.<br/>
sharpen edges: [1.0] Only sharpens edges instead of textures like skin or cloth. Avoids sharpening artifacts too much.<br/>
crispen edges: [1.0] A tamed version of FineSharp, a sharpener originally by Didée that attempts to keep local energy close to the original. Better used with higher quality sources because it sharpens artifacts.
thin edges: [1.0] As its name implies. Good for SD Anime or cartoons.
enhance detail: [1.0] Sharpens textures like skin or cloth, also sharpens artifacts.
LumaSharpen: [0.65] Blurs the original pixel with the surrounding pixels and then subtracts the blur. Avoids sharpening artifacts.
AdaptiveSharpen: [0.5] Tries to sharpen medium sharp edges the most, it avoids sharpening near flat areas and very sharp edges. From [bacondither](http://tinyurl.com/pmmn6gv)
activate anti-ringing filter: A post process method to reduce ringing that runs after each ringing sharpener.
SuperRes: [3] This is a post process method. From [Shiandow](http://tinyurl.com/kh8lta5)
----use linear light: Ideally use the same method that the source was originally downscaled with when it was mastered. Saddly this is usually not known. When enabled the image may be slightly darker and dark lines slightly fatter.<br/>
Calculate an initial guess (using the configured upscaler)<br/>
Downscale and calculate differences with original image.<br/>
Scale those differences to the final size (SoftCubic50)<br/>
Improve guess by:<br/>
Softening the image<br/>
Subtracting differences with the original image<br/>
Sharpening<br/>
Removing aliasing<br/>
Removing ringing<br/>
Repeat steps 2-4 several times.<br/>


rendering
----------


general settings:<br/>
delay playback start until render queue is full: [Disabled] Pauses playback until all the buffers are full. With this option disabled only the present buffers need to fill before playback starts.<br/>
enable windowed overlay (Windows 7 and newer): [Disabled] Only available on Nvidia and Intel GPUs. Uses a low level overlay method which bypasses the GPU LUT (monitor profile) so madVR emulates it when using this option, this is done in 16-bit so madVR can provide better quality than the GPU. Overlay also bypasses the OS to a large extent; screen-shots are not possible. D3D9 Only.
enable automatic fullscreen exclusive mode: [Enabled] madVR has exclusive access to the display. This is the most stable mode for madVR as it has the most control over when and how video frames are displayed. There is a slight flicker as madVR enters and exits this mode. Required for >8 bit output.
disable desktop composition (Vista and Windows 7): [Disabled] Disables Aero which has its own v-sync that can conflict with madVR’s. This option cannot disable desktop composition on Windows 8 or 10 but desktop composition also works better on 8 and 10.
use Direct3D 11 for presentation (Windows 7 and newer): [Disabled] Use Direct3D 11 instead of D3D9. Requires a restart of madVR to take effect. Required for >8 bit output. Overrides windowed overlay.
present a frame for every VSync: [Enabled] when disabled madVR only presents new frames when needed, relying on D3D11 to repeat frames for each VSync. Disabled may improve performance but may also cause presentation glitches.
use a separate device for presentation (Vista and newer): [Disabled] Might improve performance slightly, or it might hurt it slightly.
use a separate device for DXVA processing (Vista and newer): [Disabled] Might improve performance slightly, or it might hurt it slightly.
CPU queue size: [16] The buffer in system memory for decoded video and xySubFilter subtitles.
GPU queue size: [8] The buffer in the graphics memory for madVR’s rendering.

windowed and exclusive mode settings:<br/>
present several frames in advance: [Enabled] Uses a new method for presenting frames in advance instead of using a back-buffer queue.<br/>
how many video frames shall be presented in advance or how many backbuffers shall be used: [8 or 3] A final buffer after madVR is done rendering.<br/>
when and how shall the GPU be flushed: [flush, flush & wait (sleep), don't flush, don't flush] You need a 'flush & wait' step for '... after last render step' to be able to display rendering times in the OSD.<br/>

stereo 3d: [Disabled]<br/>
present several frames in advance: Allow madVR to output stereoscopic 3D content. 3D output is currently limited to 1080p23 with smooth motion automatically disabled.<br/>
when playing 2d content: Change the stereo 3D setting in the OS when playing 2D content.<br/>
when playing 3d content: Change the stereo 3D setting in the OS when playing 3D content. Depending on the display and GPU, 3D support may not need to be enabled in the OS to display 3D content.<br/>

smooth motion: [Disabled]<br/>
Uses frame blending to perfectly display the video’s frame rate at the display’s refresh rate. This reduces motion judder in exchange for increased blurring due to the frame blending. It has less blurring the higher the refresh rate of the display.<br/>

dithering:<br/>
Dithering is performed as the very last step in madVR to convert its internal 16 bit data to the bit depth set for the display. Any time madVR does anything to the video high bit depth information is created and dithering allows much of this information to be preserved when displayed at a lower bit depth. For example, the conversion of 8-bit YCbCr to RGB generates >8-bit RGB data. The higher the output bit-depth, as set in madVR's 'devices' -> 'properties', the lower the visible dithering noise.
None: Only use for testing, it is never useful for normal use, banding
Random Dithering: A high noise no pattern very fast option.
Ordered Dithering: [Default] This option has the lowest visible dithering noise. It uses a fixed dither texture that was optimized for low visible noise. This offers high quality dithering with a low performance hit.<br/>
Error Diffusion: Use Direct-Compute to perform very high quality error diffusion dithering. Test option 1 and 2 for yourself (or pick one randomly). They are both very good and my preference seems to change depending on the display.<br/>
use colored noise: [Enabled] Uses an inverted dither pattern for Green which reduces luma noise but adds chroma noise. You can see colored noise on a gray scale test pattern even with this option disabled if you use a 3DLUT because the 3DLUT adds color information and dithering is performed after it.
change dither for every frame: [Enabled] Uses a new dither seed for every frame or, for ordered dithering, adds random offsets and rotate the dither texture 90° between every frame.<br/>

trade quality for performance:<br/>
These options are sorted based on their impact on quality with the options that have the least quality lost for the performance gained at the top.<br/>
[Defaults to all enabled from the top down up to, and including, "don't rerender frames when fade in/out is detected"]<br/>


More advanced topics
---------------------

Toggle the On Screen Display by pressing Ctrl-J. The sum of the average stats "deinterlace" (if present), "rendering", and "present" should be a bit below the frame time in the line "v-sync [X] ms, frame [Y] ms" to avoid dropped frames and presentation glitches.<br/>

Profiles:<br/>
Right click on a device in 'devices' or the 'processing', 'scaling algorithms', or 'rendering' settings folder to create a profile group. You can only add settings pages to a group when creating it. There can only be one profile in a profile group when deleting it.<br/>
configure profile rules

Rotation support:<br/>
madVR will automatically rotate the video if rotation is specified in the video container, rotation can also be controlled manually.<br/>
The default keyboard shortcuts for rotation are:
Control + Shift + Alt + Right Arrow | Clockwise
Control + Shift + Alt + Left Arrow | Counterclockwise

IVTC and Deinterlacing:<br/>
Shortcut keys to force auto deinterlacing, DXVA2 deinterlacing, or CPU based IVTC. Forcing a deinterlacing mode also forces deinterlacing to 'on' instead of 'auto'.
Control + Shift + Alt + D | Toggle Deinterlacing: [Auto], On, Off
Control + Shift + Alt + T | Toggle Mode: [Auto], DXVA2 Deinterlacing, madVR's CPU IVTC

File name tags:<br/>
madVR will look at the folder and file names for tokens or "magic words" that tell it to treat a particular file differently.
example: "D:\Movies\TV Rips levels=tv\Broken PAL Rips matrix=PAL\my broken rip from the 90s deband=high.mkv"<br/>

Possible file name tags include:<br/>
frame rate: frameRate=24p, 24i, 24fps, 24Hz, etc. *refreshRate= is synonymous<br/>
deinterlacing: deint=On|Off|Video|Film|IVTC<br/>
debanding: deband=off|low|medium|high<br/>
profile: profile='profile name'<br/>
matrix: matrix=2020|709|601|NTSC|PAL|YCgCo|240M<br/>
primaries: primaries=2020|DCI|709|SmpteC|EBU|sRGB|NTSC|PAL|470M|240M|170M<br/>
levels: levels=PC|TV|fullrange|limited|doubleExp|tripleExp *range= is synonymous<br/>
blacklevel: blacklevel=X, X=-50 to +50<br/>
whitelevel: whitelevel=X, X=-50 to +50<br/>
contrast: contrast=X, X=-100 to +100<br/>
brightness: brightness=X, X=-100 to +100<br/>
saturation: blacklevel=X, X=-100 to +100<br/>
hue: hue=X, X=-180 to +180<br/>

madVR can decimate progressive streams:<br/>
e.g. 720p60/720p50 broadcast with 24p/25p content. Press control+alt+shift+d to enable deinterlacing and press control+alt+shift+t to force decimation on. It has the same limitations as madVR's IVTC or film mode.<br/>

Known Limitations or Complications:<br/>
-madVR's 3D support is currently limited to 1080p23.<br/>
-When using a 3DLUT madVR can generate out of gamut values to display WtW information unless using 'enable windowed overlay', in which case WtW information is clipped.<br/>
-NNEDI3 will not run on Windows XP because it is missing the OpenCL D3D11 Interop.<br/>
-Native DXVA decoding has some negative ramifications such as it is impossible to use force film (IVTC) or xy/vsfilter for subtitles.<br/>
-madVR IVTC can detect a lot of cadences but can "only" handle some of them correctly. For example the rare cadence 3:2:3:2:2 (25 fps in 30i 60 fields) does not work well.<br/>
-madVR currently always switches to 23Hz when having forced film mode on while playing 59i content, this is often optimal, but not always. With no good way for madVR to know it goes with 23 Hz.<br/>

Theoretical rendering path:<br/>
It is oversimplified and a lot of what madVR does is not included. See screenshots folder.<br/>
