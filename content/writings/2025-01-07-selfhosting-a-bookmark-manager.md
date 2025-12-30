+++
title = "Bookmark Management with Linkding: A Self-Hosted Guide"

[taxonomies]
tags = ["selfhosting", "linux"]

[extra]
toc = false
+++

<div class="center">
<img src="/img/blogs/linkding.webp" alt="linking ui">
</div>

### Introduction

The internet offers a wealth of resources, but only a handful truly grab our attention. Sadly, these gems often vanish into the vast web abyss if not carefully bookmarked. Personally, I’ve relied on my browser’s bookmarks folder for years. While convenient, searching through this growing list often becomes an arduous task.

I previously used [Omnivore](https://omnivore.app/), a "read it later" application, until it shut down last year. This led me to explore bookmark managers. Although I found plenty of great options like [Are.na](https://www.are.na/), [Hoarder](https://hoarder.app/), and [Linkwarden](https://linkwarden.app), the one that truly caught my eye was [Linkding](https://linkding.link/). Its simplicity stood out, and since adopting it, managing my bookmarks has been a seamless experience.

In this blog, I’ll walk you through how to set up Linkding on your own server.

### Setting Up Linkding

The setup is straightforward if you follow the [official documentation](https://linkding.link/installation/). All you need is a simple Docker Compose configuration. Below is an example:

```yaml
services:
  linkding:
    container_name: "${LD_CONTAINER_NAME:-linkding}"
    image: sissbruecker/linkding:latest
    ports:
      - "${LD_HOST_PORT:-9090}:9090"
    volumes:
      - "${LD_HOST_DATA_DIR:-./data}:/etc/linkding/data"
    env_file:
      - .env
    restart: unless-stopped
```

### Creating a Superuser

To create a superuser, you can use the following command while the container is running:

```bash
docker exec -it linkding python manage.py createsuperuser --username=joe --email=joe@example.com
```

Alternatively, define the superuser credentials in the `.env` file:

```env
LD_SUPERUSER_NAME=myusername
LD_SUPERUSER_PASSWORD=mypassword
```

### Accessing the UI

Once your container is running, you can access the Linkding UI at **http://localhost:9090**. Log in using the credentials you set up, and you’re good to go! Additionally, you can install the [Linkding browser extension](https://chromewebstore.google.com/detail/linkding-extension/beakmhbijpdhipnjhnclmhgjlddhidpe) to start saving links effortlessly.

### Enhancing Linkding with Add-Ons

### Linkding Injector

<div class="center">
<img src="/img/blogs/linkding-inj.webp" alt="linking ui">
</div>

[Linkding Injector](https://github.com/Fivefold/linkding-injector) is a browser extension that displays your saved bookmarks directly in your search engine results. It’s easy to set up by following the instructions in the repository.

### Mobile Integration with HTTP Shortcuts

If you frequently use your mobile to save links, Linkding has you covered! Install the [HTTP Shortcuts](https://f-droid.org/packages/ch.rmy.android.http_shortcuts/) app from F-Droid. Here’s how to set it up:

- Open the app and go to the three-dot menu in the top-right corner.
- Select **Import/Export**, then choose **Import from URL**.
- Enter this URL:

  ```
  https://raw.githubusercontent.com/sissbruecker/linkding/refs/heads/master/docs/src/assets/linkding_shortcut.json
  ```

- After importing, go back to the main screen, open the three-dot menu again, and select **Variables**.
- Update the **linkding_instance** and **linkding_api_key** variables with your self-hosted instance details.

Now, when you share a link from your browser, choose **HTTP Shortcuts**, select **Linkding**, and optionally add tags or save it as untagged.

### Backing Up Your Bookmarks

Backups are essential for any server. You can automate this process using a shell script and a cronjob. The following commands create a backup of your Linkding database:

```bash
docker exec -it linkding python manage.py full_backup /etc/linkding/data/backup.zip
docker cp linkding:/etc/linkding/data/backup.zip backup.zip
```

Schedule this as a cronjob to ensure your data is always safe.

### Conclusion

Linkding offers a simple, efficient, and self-hosted solution for bookmark management. From its intuitive UI to useful extensions and mobile integrations, it’s a tool that enhances the way you save and organize your favorite online resources. With regular backups in place, you can rest assured that your bookmarks are safe and accessible whenever you need them.
