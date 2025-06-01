FROM pipech/erpnext-docker-debian:version-15-latest

# These variable has been set from base image
# $systemUser, $benchFolderName
USER $systemUser
WORKDIR /home/$systemUser/$benchFolderName

# Copy sites folder, we'll mount volume over this folder
# then we could copied the sites folder to the mounted volume
RUN cp -r /home/$systemUser/$benchFolderName/sites /home/$systemUser/$benchFolderName/sites-initial \
    && cp -r /home/$systemUser/$benchFolderName/apps /home/$systemUser/$benchFolderName/apps-initial
