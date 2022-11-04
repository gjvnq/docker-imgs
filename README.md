# docker-imgs
Various docker images I needed to make or change

Conventions:

  * Applications are run as le_app user and le_app group
  * Arguments `LE_APP_UID` and `LE_APP_GID` specify the le_app user/group UID/GID. (10001 by default)
  * Pretty much everything runs on HTTP only by default. The traffic encryption is left to container user to set up with a proxy