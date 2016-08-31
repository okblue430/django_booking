# django_booking

Add booking to your INSTALLED_APPS
-----
INSTALLED_APPS = (
    ...,
    'booking',
)
Add the booking URLs to your urls.py

urlpatterns = patterns('',
    ...
    url(r'^booking/', include('booking.urls')),
)
Don't forget to migrate your database

./manage.py migrate booking

Usage
-----

If you allow anonymous bookings, the session object is stored within the booking model. Otherwise it will be connected to the User model.

NOTE: If a session is destroyed, the connected booking model will also be removed.

In order to allow login via email and booking ID, please add this to your 

``AUTHENTICATION_BACKENDS``::

AUTHENTICATION_BACKENDS = (
    # your usual auth backends
    'booking.auth_backends.BookingIDBackend',
)
At the moment you will have to write a new view that will render the booking.forms.BookingIDAuthenticationForm. If the form is valid, your view should call auth_login(request, form.get_user()), similar to Django's original login view.
