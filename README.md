# SubPlayer

> SubPlayer is an online subtitle editor

![Screenshot](./images/screenshot6.png)

## Homepage

[https://subplayer.js.org](https://subplayer.js.org)

## Donations

We accept donations through these channels:

![pay](./public/pay.png)

-   [Paypal](https://www.paypal.me/harveyzack)

# SubPlayer Youtube Integration
As mentioned, Youtube Integration has been added to SubPlayer

```
yarn
```
to install the node_modules/

```javascript
<div className="btn" style={{ width: '100%' }}>
    <Translate value="OPEN VIDEO" />
    <button className="file" type="file" onClick={handleSubmit} />
</div>
```
The Above code is added, To add a Button to prompt the user to input the Youtube Video URL

Now we have to handle the Button, to fetch the youtube video and subtitles from the API

```javascript
const handleSubmit = async () => {
        let videoURL = prompt('Input video URL');
        if (!videoURL) return;

        setLoading(t('LOADING_VIDEO'));
        const res = await fetch(
            `https://youtube-dl-utils-api.herokuapp.com/get_youtube_video_link_with_captions?url=${videoURL}`,
        );
        const data = await res.json();
        waveform.decoder.destroy();
        waveform.drawer.update();
        waveform.seek(0);
        player.currentTime = 0;
        const subs = await fetch(data.subtitles).then((res) => res.text());
        const url = vtt2url(subs);
        const sub = await url2sub(url);
        setSubtitle(sub);
        player.src = data.video;
        setLoading('');
};
```
We are converting the Subtitles from text to vtt to add it to the Player.

## QQ Group

![QQ Group](./public/qqgroup.png)

## License

MIT © Harvey Zack
