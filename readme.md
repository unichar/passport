# Passport.js authentication for UniChar

[Passport](http://passportjs.org/) strategy for authenticating with [UniChar](https://unichar.net/) using the OAuth 2.0 API.

This module lets you authenticate using UniChar in your Node.js applications.

By plugging into Passport, UniChar authentication can be easily and unobtrusively integrated into any application or framework that supports [Connect](http://www.senchalabs.org/connect/)-style middleware, including [Express](http://expressjs.com/).

## Install
```
npm install passport-unichar
```

## Usage

#### Configure Strategy

The UniChar authentication strategy authenticates users using a UniChar account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which accepts these credentials and calls `done` providing a user, as well as `options` specifying a client ID, client secret, and callback URL.
```
passport.use(new UniCharOAuth2Strategy({
	clientID: CLIENT_ID,
	clientSecret: CLIENT_SECRET,
	callbackURL: "https://www.example.net/auth/unichar/callback"
	},
	function(accessToken, refreshToken, profile, done) {
	User.findOrCreate({ providerId: profile.id }, function (err, user) {
		return done(err, user);
	});
	}
));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'unichar'` strategy, to authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/) application:

```
app.get('/auth/unichar',
	passport.authenticate('unichar'));

app.get('/auth/unichar/callback',
	passport.authenticate('unichar', { failureRedirect: '/login' }),
	function(req, res) {
	// Successful authentication, redirect home.
	res.redirect('/');
	});
```

## Credits

Initiated by [Makis Tracend](http://github.com/tracend)

Part of [UniChar](http://unichar.net/) by [K&D Interactive](http://kdi.co/)

Released under the [MIT license](http://makesites.org/licenses/MIT)

