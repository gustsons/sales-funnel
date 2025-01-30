import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { motion } from "framer-motion";

export default function SalesFunnel() {
  const [email, setEmail] = useState("");
  const [submitted, setSubmitted] = useState(false);
  const [error, setError] = useState("");

  const handleSubmit = () => {
    if (!email.trim()) {
      setError("Email is required");
      return;
    }
    if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) {
      setError("Enter a valid email address");
      return;
    }
    setError("");
    setSubmitted(true);
    console.log("Email submitted:", email);
  };

  return (
    <div className="flex flex-col items-center justify-center min-h-screen bg-gray-900 text-white p-6">
      <motion.h1
        className="text-4xl font-bold mb-6 text-center"
        initial={{ opacity: 0, y: -20 }}
        animate={{ opacity: 1, y: 0 }}
      >
        AI-Driven Business Growth
      </motion.h1>
      <motion.p
        className="text-lg mb-8 text-center max-w-xl"
        initial={{ opacity: 0 }}
        animate={{ opacity: 1 }}
        transition={{ delay: 0.3 }}
      >
        Learn how AI can optimize your business, increase efficiency, and scale with precision. Enter your email to get exclusive insights.
      </motion.p>
      <Card className="w-full max-w-md p-6 bg-gray-800">
        <CardContent>
          {!submitted ? (
            <div className="flex flex-col items-center">
              <Input
                type="email"
                placeholder="Enter your email"
                value={email}
                onChange={(e) => setEmail(e.target.value)}
                className="mb-2 w-full p-3 rounded-lg bg-gray-700 text-white border border-gray-600 focus:ring-2 focus:ring-blue-500"
              />
              {error && <p className="text-red-500 text-sm mb-2">{error}</p>}
              <Button onClick={handleSubmit} className="w-full bg-blue-600 hover:bg-blue-700">
                Get Insights
              </Button>
            </div>
          ) : (
            <motion.p
              className="text-center text-green-400 text-lg"
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
            >
              Thank you! Check your inbox for exclusive insights.
            </motion.p>
          )}
        </CardContent>
      </Card>
    </div>
  );
}
