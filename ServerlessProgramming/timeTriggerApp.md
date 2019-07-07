module.exports = function (context, myTimer) {

    var timeStamp = new Date().toISOString();

    var mymsg;

    //twilio Account credential
    const accountSid = 'AC07b2c35584aece8dbdd64dbdb873dcd8';
    const authToken = '30009f233d4bfaa7af018c4b087761cc';

    const client = require('twilio')(accountSid, authToken);

    //Check if time is past
    if (myTimer.IsPastDue) {
        context.log('Node is running late!');
    }

    const request = require('request');

    //Call Nasa API to get the title
    request('https://api.nasa.gov/planetary/apod?api_key=DEMO_KEY', { json: true }, (err, res, body) => {
        if (err) { return console.log(err); }
        mymsg = body.title;
        //context.log(body.title);
        sms(mymsg);
    });
    
    function sms(msg) {

        //context.log(msg);

        client.messages.create({
            to: '+64276497612',
            from: '+12565790843',
            body: msg
        })  
    }

};