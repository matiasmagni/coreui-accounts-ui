# Universe Accounts UI

Accounts UI replacement for Universe using React for the CoreUI (https://github.com/matiasmagni/coreui-meteor-react) Bootstrap Admin Template. 

## Installation

	In order to install this package you must do it inside a coreui-meteor-react boilerplate (https://github.com/matiasmagni/coreui-meteor-react). If you don't have it already, you must download it first:
	
	$ git clone https://github.com/matiasmagni/coreui-meteor-react
	$ cd coreui-meteor-react

	Then you can add the package inside de project:
	
    $ meteor add mmagni:coreui-accounts-ui

- This package assumes that you're using React
- This package uses CoreUI styling classes.

- Login options will show based on installed packages and you need to add them manually, e.g.
    * `meteor add accounts-password accounts-facebook ...`

## Usage

- You need to set up own routes
- Place `accounts-ui` components where you wish to render forms

Basic usage could look like:

    import {ComboBox} from 'meteor/universe:accounts-ui';

    Router.route('/login', {
        name: 'login',
        action () {
            mount(Layout, {
                content: <ComboBox />
            });
        }
    });

### Available components

- `LoginBox` - simple login form
- `RegisterBox` - simple register form
- `ComboBox` - both above forms combined into one
- `ResetPasswordBox` - password reset form
- `EnrollmentBox` - password init form

## Configuration

No config yet, but will have similar configuration to `accounts-ui`.

## Know issues

- Has UI for password reset, but don't provide server-side functionality yet.
- You need to set ServiceConfiguration options for external services on your own, no forms yet

## Examples

### EnrollmentBox

```javascript
import {EnrollmentBox} from 'meteor/universe:accounts-ui';

Accounts.onEnrollmentLink((token, done) => {
    Meteor.setTimeout(() => { // to mount after FlowRouter (you can also use Accounts.urls.enrollAccount)
        const onComplete = () => {
            done();
            FlowRouter.go('/');
        };
        mount(MainLayout, {
            content: <EnrollmentBox token={token} onComplete={onComplete} />
        });
    }, 100);
});```
