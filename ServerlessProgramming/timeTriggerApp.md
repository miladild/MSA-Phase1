module.exports = async function (context, myTimer) {


    const accountSid = 'AC07b2c35584aece8dbdd64dbdb873dcd8';
    const authToken = '30009f233d4bfaa7af018c4b087761cc';

    const client = require('twilio')(accountSid, authToken);

    var timeStamp = new Date().toISOString();
    
    if (myTimer.IsPastDue)
    {
        context.log('JavaScript is running late!');
    }

      client.messages.create({
        to: '+64276497612',
        from: '+12565790843',
        body:'Just a 5 minute reminder to keep your posture up'
    })  
};