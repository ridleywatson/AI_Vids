import requests

access_token = "YOUR_ACCESS_TOKEN"
instagram_user_id = "YOUR_INSTAGRAM_USER_ID"

def post_video(video_path, caption):
    # Step 1: Upload the video to Instagram
    upload_url = f"https://graph.facebook.com/v19.0/{instagram_user_id}/media"
    payload = {
        'video_url': 'https://yourserver.com/path-to-video.mp4',
        'caption': caption,
        'access_token': access_token
    }
    response = requests.post(upload_url, data=payload)
    result = response.json()
    
    # Step 2: Publish it
    creation_id = result['id']
    publish_url = f"https://graph.facebook.com/v19.0/{instagram_user_id}/media_publish"
    publish_response = requests.post(publish_url, data={
        'creation_id': creation_id,
        'access_token': access_token
    })
    return publish_response.json()
