---
title:
menu: Accueil

form:
    name: courriels
    action: /home
    fields:
        - name: name
          label: Nom
          placeholder: Saisissez votre nom
          autocomplete: on
          type: text
          validate:
            required: true

        - name: email
          label: Courriel
          placeholder: Saisissez votre adresse courriel
          type: text
          validate:
            rule: email
            required: true

        - name: message
          label: Message
          size: long
          placeholder: Saisissez votre message
          type: textarea
          validate:
            required: true

    buttons:
        - type: submit
          value: Envoyer
          class: submit

    process:
        - email:
            from: "{{ form.value.email|e }}"
            to:
              - "{{ config.plugins.email.to }}"
              - "{{ form.value.email|e }}"
            subject: "[Feedback] {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - save:
            fileprefix: feedback-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - message: Thank you for your feedback!
        - display: thankyou

onpage_menu: true
content:
    items: @self.modular
    order:
        by: manuel
        dir: asc
        custom:
            - _about
            - _resume
            - _portfolio
            - _contact
---
