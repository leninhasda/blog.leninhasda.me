---
title: লিনাক্স টার্মিনালে কিভাবে git branch name দেখাবেন
template: templates/post.pug
date: 2015-08-11
author: Lenin Hasda
keywords: git, terminal, hack, branch name, git command, git branch
---

অনেক ভিডিও টিউটোরিয়ালে দেখেছি তারা যখন ম্যাক টার্মিনালে লেখে তখন গিট (Git) এর branch name দেখায়। লিনাক্স (উবুন্টু) টার্মিনালে এ সুবিধাটি সুরু থেকে দেয়া থাকে না। বেশ কিছুক্ষন খোজার পর ছোট একটা টিউটোরিয়াল পেয়েছি যা আমার কালেকশনে রাখতেসি এবং আপনাদের সাথেও শেয়ার করছি 🙂

![show](/img/3_show.png)

উপরের ছবিতে দেখতে পাচ্ছেন আমার টার্মিনালে branch name দেখাচ্ছে। এ কাজটি করা এক্কেবারে সহজ। এজন্য প্রথমে আপনাকে .bashrc ফাইলটি ওপেন করে নিচের লাইন গুলো অ্যাড করে দিতে হবে।

```bash
# Add git branch if its present to PS1
parse_git_branch() {
   git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
if [ "$color_prompt" = yes ]; then
   PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '
else
   PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w$(parse_git_branch)\$ '
fi
unset color_prompt force_color_prompt
```

যেকোন জাগায় দিলেই হবে। আমার ফাইলে আমি ৫৯-৬৮ লাইনে দিয়েছি। টার্মিনাল বন্ধ করে আবার ওপেন করুন, এর পর থেকে আপনি যতবার গিট প্রোজেক্টে যাবেন আগে থেকেই আপনাকে branch name দেখাবে 🙂

**কিছু এক্সট্রা:**    
আপনি যদি আমার মতো কালার পেলেট চান তাহলে আপনাকে আরও দুটো কাজ করতে হবে। একটু লক্ষ্য করলে দেখবেন যে লাইন গুলো আপনি দিয়েছেন প্রায় একই রকম কিছু লাইন .bashrc তে আগে থেকেই আছে। আপনাকে সেগুলা মুছে দিতে হবে অথবা আমার মত কমেন্ট করে রাখতে হবে। আমার ফাইলে আমি ৭০-৭৫ লাইনে আমি কমেন্ট করে রেখেছি।
এরপর force_color_prompt=yes লাইনটি আন-কমেন্ট করতে হবে। আমার ৪৬ লাইনে যা আমি করেছি।

আশা করছি এরপর থেকে আপনাকে আর বার বার git branch দিয়ে branch name দেখতে হবে না বা ভুল কোন ব্রাঞ্চ এও কমিট করবেন না। আপানর ব্রাঞ্চ নেম টার্মিনালেই সব সময় দেখতে পাবেন 🙂


------


**Ref:**

* https://www.leaseweblabs.com/2013/08/git-tip-show-your-branch-name-on-the-linux-prompt/

