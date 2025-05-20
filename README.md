// Music Sharing Platform - Enhanced Core // Tech: React + TailwindCSS + Framer Motion // Future-Ready for Firebase, Upload Panel, Auth

import React, { useState } from "react"; import { Card, CardContent } from "@/components/ui/card"; import { Button } from "@/components/ui/button"; import { Input } from "@/components/ui/input"; import { Textarea } from "@/components/ui/textarea"; import { Music, Download, Heart, Share2, CheckCircle, UploadCloud, User } from "lucide-react"; import { motion, AnimatePresence } from "framer-motion";

const songs = [ { id: 1, title: "Heavenly Tune", artist: "Lixz Edits", url: "/songs/heavenly_tune.mp3", cover: "/covers/cover1.jpg", }, { id: 2, title: "Royal Vibes", artist: "Lixz Edits", url: "/songs/royal_vibes.mp3", cover: "/covers/cover2.jpg", }, ];

export default function MusicShareSite() { const [likes, setLikes] = useState({}); const [comment, setComment] = useState(""); const [showThanks, setShowThanks] = useState(false);

const handleLike = (id) => { setLikes((prev) => ({ ...prev, [id]: (prev[id] || 0) + 1 })); };

const handleSupportConfirm = () => { setShowThanks(true); setTimeout(() => setShowThanks(false), 4000); };

return ( <div className="min-h-screen bg-gradient-to-br from-black via-gray-900 to-black text-white p-6 relative overflow-hidden"> <div className="absolute inset-0 opacity-10 blur-2xl bg-[url('/bg-luxury-pattern.png')] bg-cover bg-no-repeat z-0"></div>

<motion.header
    className="flex items-center justify-between mb-8 z-10 relative"
    initial={{ opacity: 0, y: -50 }}
    animate={{ opacity: 1, y: 0 }}
    transition={{ duration: 1 }}
  >
    <h1 className="text-4xl font-bold text-yellow-300">Lux Music Hub</h1>
    <div className="flex gap-4">
      <Button variant="outline" className="flex items-center gap-2">
        <User className="w-4 h-4" /> Login / Sign Up
      </Button>
      <Button variant="secondary" className="flex items-center gap-2">
        <UploadCloud className="w-4 h-4" /> Upload Song
      </Button>
    </div>
  </motion.header>

  <motion.div
    className="grid md:grid-cols-2 gap-8 z-10 relative"
    initial={{ opacity: 0 }}
    animate={{ opacity: 1 }}
    transition={{ delay: 0.5, duration: 1 }}
  >
    {songs.map((song) => (
      <motion.div
        key={song.id}
        whileHover={{ scale: 1.03 }}
        transition={{ type: "spring", stiffness: 200 }}
      >
        <Card className="bg-white/10 backdrop-blur-xl rounded-2xl shadow-2xl p-4 border border-yellow-300">
          <CardContent>
            <img
              src={song.cover}
              alt={song.title}
              className="rounded-xl mb-4 w-full h-48 object-cover shadow-md"
            />
            <h2 className="text-2xl font-semibold text-yellow-200">{song.title}</h2>
            <p className="text-sm text-gray-300">by {song.artist}</p>

            <audio controls className="w-full my-4">
              <source src={song.url} type="audio/mpeg" />
              Your browser does not support the audio element.
            </audio>

            <div className="flex gap-4 items-center mb-2">
              <Button onClick={() => handleLike(song.id)} variant="ghost" size="icon">
                <Heart className="text-red-500" />
              </Button>
              <span>{likes[song.id] || 0} Likes</span>

              <Button variant="ghost" size="icon">
                <Download className="text-blue-400" />
              </Button>

              <Button variant="ghost" size="icon">
                <Share2 className="text-green-400" />
              </Button>
            </div>

            <Textarea
              placeholder="Leave a comment..."
              className="bg-black/30 text-white"
              value={comment}
              onChange={(e) => setComment(e.target.value)}
            />

            <div className="mt-4 text-sm text-gray-300">
              <p>If you love this track, support me via UPI:</p>
              <img
                src="/upi-qr.png"
                alt="UPI QR Code"
                className="w-32 mt-2 rounded-md border border-yellow-400"
              />
              <p className="text-yellow-300 mt-1 font-mono">lixzedits@upi</p>
              <Button
                onClick={handleSupportConfirm}
                className="mt-2 bg-yellow-500 text-black hover:bg-yellow-400"
              >
                I’ve Paid
              </Button>
            </div>
          </CardContent>
        </Card>
      </motion.div>
    ))}
  </motion.div>

  <AnimatePresence>
    {showThanks && (
      <motion.div
        initial={{ opacity: 0, scale: 0.8 }}
        animate={{ opacity: 1, scale: 1 }}
        exit={{ opacity: 0, scale: 0.8 }}
        className="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center z-50"
      >
        <motion.div
          className="bg-white p-6 rounded-2xl shadow-lg text-black text-center"
          initial={{ y: 50 }}
          animate={{ y: 0 }}
          exit={{ y: 50 }}
        >
          <CheckCircle className="text-green-500 w-12 h-12 mx-auto mb-2" />
          <h2 className="text-xl font-semibold">Thank You!</h2>
          <p>Your support keeps the music flowing.</p>
        </motion.div>
      </motion.div>
    )}
  </AnimatePresence>

  <motion.footer
    className="mt-12 text-center text-gray-400 text-sm z-10 relative"
    initial={{ opacity: 0 }}
    animate={{ opacity: 1 }}
    transition={{ delay: 1.5 }}
  >
    © 2025 Lux Music Hub | Built by Lixz Edits
  </motion.footer>
</div>

); }
